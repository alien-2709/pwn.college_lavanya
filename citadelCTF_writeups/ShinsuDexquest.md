*As you climb the path, a guardian emerges, its form shifting between the visage of a long-dead climber and a metallic sentinel.*  

*It moves with a strange grace, holding out a cartridge containing a single file.*   
 
*You realize the file is compatible with the device you carry and may be the key to continue your ascent toward the Citadel’s heart.*  

## What I did:
1.The file give *dexquest.apk* is an android application package.  
2.I downloaded it on my phone and opened it .  
3.There were 3 pages I could see - Observer ,The introduction page and the Shinsu Barrier.  
4.Decompile the APK with JADX to readable Java/Kotlin-like sources.  
```
./bin/jadx -d ~/dexquest_out /mnt/c/Users/drsan/Downloads/dexquest.apk
INFO  - loading ...
INFO  - processing ...
ERROR - finished with errors, count: 23
```
5.Next,we listed the app package : I used A.I to find the right commands for this part and the relevant keyworks as well.
```
ls -d ~/dexquest_out/sources/* | sed -n '1,200p'
```
```
cd ~/dexquest_out/sources
grep -R -n -iE "vault|flag|verify|check|validate|unlock|password|citadel|keycode|submit" . | sed -n '1,200p'
```
```
cd ~/dexquest_out/sources
grep -R -n --exclude-dir=android --exclude-dir=kotlin -iE "com/shinsu|dexquest|vault|flag|verify|check|validate|unlock|password|citadel|keycode|submit" . | sed -n '1,200p'
```
6.we found the app package (com.shinsu.dexquest) and Vault.java is present.
```
~/dexquest_out/sources$ nl -ba ~/dexquest_out/sources/com/shinsu/dexquest/screens/Vault.java | sed -n '1,400p'

```
7.That prints the first 400 numbered lines of Vault.java.   
8.In order to obtain the 99-digit string that acts as passcode to the vault , the rest must also be printed.
```
nl -ba ~/dexquest_out/sources/com/shinsu/dexquest/screens/Vault.java | sed -n '401,999p'
```
9.This printed the required lines . Next , I utilised A.I. which extracted the entire check routine and reconstructed the 99-digit num that makes green == 99. If you submit that exact string to the Vault, the code sets Vault.password = input (so the app records the password), which is the next piece we need to turn into the citadel{...} flag.
That string was 
```
2464511210365282026238901200112222498714684815355211850969748918921930947358058258074789422723982625
```
10.In order to inspect the dexquest.apk file for code to understand how it works , we run:
```
 nl -ba ~/dexquest_out/sources/com/shinsu/dexquest/screens/Observer.java | sed -n '1,400p'
```
The Observer simply navigates you to the Vault; the Vault saved the 99-digit string into Vault.password. Now we need to find where that password is used elsewhere (some other class should read Vault.getPassword() or Vault.password and turn it into the citadel{...} flag).  

11.Search for any references to getPassword, Vault.password, or Vault.getPassword:
```
cd ~/dexquest_out/sources
grep -R -n --exclude-dir=android --exclude-dir=kotlin -iE "Vault.getPassword|Vault\.password|getPassword\\(" . | sed -n '1,200p'


```
12.Search for any uses of the literal password (to catch references that don't use Vault.* explicitly):
```
 grep -R -n --exclude-dir=android --exclude-dir=kotlin -i "password" . | sed -n '1,200p'
```
Through this , NextRoom.java references Vault.INSTANCE.getPassword() directly. That’s exactly where the numeric password is turned into bytes and probably used to build the flag.  

13.Inspect Nextroom.java code to find where the flag could be:  
```
nl -ba ~/dexquest_out/sources/com/shinsu/dexquest/screens/NextRoom.java | sed -n '1,500p'
```
So the final flag depends entirely on the runtime value of Vault.password. In Vault.java that field is only assigned when green == 99 (i.e. when the 99-digit check passes).  

14.However the string that was extracted by A.I earlier did not get submitted in the app and thus , I wasnt able to move to the next room where the flag is present . After trying multiple times , the app still wouldnt accept all 99 digits i.e. green didn't reach 99 . Thus , I utilised A.I to create a python script that can compute the exact error in the original script and give me the correct passcode .  
I saved the below .py file as check_vault.py.
```
# create and run the helper script
cat > ~/tools/check_vault.py <<'PY'
#!/usr/bin/env python3
import re, sys, subprocess
from pathlib import Path

# path to decompiled Vault.java - adjust if your jadx output is elsewhere
vault_path = Path.home() / "dexquest_out" / "sources" / "com" / "shinsu" / "dexquest" / "screens" / "Vault.java"
if not vault_path.exists():
    print("ERROR: Vault.java not found at:", vault_path)
    print("Run this script from the same machine where you decompiled the APK and adjust the vault_path above if needed.")
    sys.exit(1)

txt = vault_path.read_text(encoding='utf-8', errors='ignore')

# Extract num.charAt(index) == 'digit' patterns
pairs = []
for m in re.finditer(r"num\.charAt\((\d+)\)\s*==\s*'(\d)'", txt):
    idx = int(m.group(1))
    digit = m.group(2)
    pairs.append((idx, digit))

# Build expected 99-char target
target = ['0'] * 99
for idx, digit in pairs:
    if 0 <= idx < 99:
        target[idx] = digit
target = ''.join(target)

print("EXPECTED (99 chars):")
print(target)
print()

# Ask user to paste the actual field content to compare (or leave blank to use clipboard)
val = input("Paste the Vault input (Select All -> Copy from the app) and press Enter:\n").strip()
if not val:
    # try to read Android clipboard via adb (optional)
    try:
        out = subprocess.check_output(["adb", "shell", "dumpsys", "clipboard"], stderr=subprocess.DEVNULL, text=True)
        # crude parse: look for "text:" or "Primary Clip"
        import re
        m = re.search(r"text:\s*(.*)", out)
        if m:
            val = m.group(1).strip()
            print("Got clipboard via adb:", val)
        else:
            print("No input and no clipboard text found (adb output may vary). Exiting.")
            sys.exit(1)
    except Exception as e:
        print("No input provided and adb clipboard attempt failed:", e)
        sys.exit(1)

print()
print("Your pasted length:", len(val))
print("Expected length:", len(target))
print("Exact match:", val == target)
print()

# Report mismatches
mismatches = []
minl = min(len(val), len(target))
for i in range(minl):
    if val[i] != target[i]:
        mismatches.append((i, target[i], val[i]))
if len(val) != len(target):
    print("Length mismatch (expected 99).")

if not mismatches and len(val)==len(target):
    print("SUCCESS: Your string matches expected exactly. Submit it in the app.")
else:
    print(f"Found {len(mismatches)} mismatches (showing up to 200):")
    for i, exp, got in mismatches[:200]:
        print(f"  index {i:02d}: expected '{exp}'  vs  actual '{got}'")
    if len(mismatches) == 0 and len(val) != len(target):
        print("No character mismatches, but length differs. Ensure no extra/missing digit.")
    print()
    print("Copy this exact 99-digit string (the expected value) and paste it into the app input, then Submit:")
    print(target)
PY

python3 ~/tools/check_vault.py
```
And then I ran it : 
```
cat > ~/tools/check_vault.py <<'PY'
#!/usr/bin/env python3
import re, sys, subprocess
from pathlib import Path

# path to decompiled Vault.java - adjust if your jadx output is elsewhere
vault_path = Path.home() / "dexquest_out" / "sources" / "com" / "shinsu" / "dexquest" / "screens" / "Vault.java"
if not vault_path.exists():
    print("ERROR: Vault.java not found at:", vault_path)
    print("Run this script from the same machine where you decompiled the APK and adjust the vault_path above if needed.")
    sys.exit(1)

txt = vault_path.read_text(encoding='utf-8', errors='ignore')

# Extract num.charAt(index) == 'digit' patterns
pairs = []
for m in re.finditer(r"num\.charAt\((\d+)\)\s*==\s*'(\d)'", txt):
    idx = int(m.group(1))
    digit = m.group(2)
    pairs.append((idx, digit))

# Build expected 99-char target
target = ['0'] * 99
for idx, digit in pairs:
    if 0 <= idx < 99:
        target[idx] = digit
target = ''.join(target)

print("EXPECTED (99 chars):")
print(target)
print()

# Ask user to paste the actual field content to compare (or leave blank to use clipboard)
val = input("Paste the Vault input (Select All -> Copy from the app) and press Enter:\n").strip()
if not val:
    # try to read Android clipboard via adb (optional)
    try:
        out = subprocess.check_output(["adb", "shell", "dumpsys", "clipboard"], stderr=subprocess.DEVNULL, text=True)
        # crude parse: look for "text:" or "Primary Clip"
python3 ~/tools/check_vault.pydigit string (the expected value) and paste it into the app input, then Submit:")
EXPECTED (99 chars):
246451121036528202623890120011222498714684815355211850969748918921930947358058258074789422723982625

Paste the Vault input (Select All -> Copy from the app) and press Enter:
246451121036528202623890120011222249871468481535521185096974891892193094735805825807478942272398262

Your pasted length: 99
Expected length: 99
Exact match: False

Found 63 mismatches (showing up to 200):
  index 33: expected '4'  vs  actual '2'
  index 34: expected '9'  vs  actual '4'
  index 35: expected '8'  vs  actual '9'
  index 36: expected '7'  vs  actual '8'
  index 37: expected '1'  vs  actual '7'
  index 38: expected '4'  vs  actual '1'
  index 39: expected '6'  vs  actual '4'
  index 40: expected '8'  vs  actual '6'
  index 41: expected '4'  vs  actual '8'
  index 42: expected '8'  vs  actual '4'
  index 43: expected '1'  vs  actual '8'
  index 44: expected '5'  vs  actual '1'
  index 45: expected '3'  vs  actual '5'
  index 46: expected '5'  vs  actual '3'
  index 48: expected '2'  vs  actual '5'
  index 49: expected '1'  vs  actual '2'
  index 51: expected '8'  vs  actual '1'
  index 52: expected '5'  vs  actual '8'
  index 53: expected '0'  vs  actual '5'
  index 54: expected '9'  vs  actual '0'
  index 55: expected '6'  vs  actual '9'
  index 56: expected '9'  vs  actual '6'
  index 57: expected '7'  vs  actual '9'
  index 58: expected '4'  vs  actual '7'
  index 59: expected '8'  vs  actual '4'
  index 60: expected '9'  vs  actual '8'
  index 61: expected '1'  vs  actual '9'
  index 62: expected '8'  vs  actual '1'
  index 63: expected '9'  vs  actual '8'
  index 64: expected '2'  vs  actual '9'
  index 65: expected '1'  vs  actual '2'
  index 66: expected '9'  vs  actual '1'
  index 67: expected '3'  vs  actual '9'
  index 68: expected '0'  vs  actual '3'
  index 69: expected '9'  vs  actual '0'
  index 70: expected '4'  vs  actual '9'
  index 71: expected '7'  vs  actual '4'
  index 72: expected '3'  vs  actual '7'
  index 73: expected '5'  vs  actual '3'
  index 74: expected '8'  vs  actual '5'
  index 75: expected '0'  vs  actual '8'
  index 76: expected '5'  vs  actual '0'
  index 77: expected '8'  vs  actual '5'
  index 78: expected '2'  vs  actual '8'
  index 79: expected '5'  vs  actual '2'
  index 80: expected '8'  vs  actual '5'
  index 81: expected '0'  vs  actual '8'
  index 82: expected '7'  vs  actual '0'
  index 83: expected '4'  vs  actual '7'
  index 84: expected '7'  vs  actual '4'
  index 85: expected '8'  vs  actual '7'
  index 86: expected '9'  vs  actual '8'
  index 87: expected '4'  vs  actual '9'
  index 88: expected '2'  vs  actual '4'
  index 90: expected '7'  vs  actual '2'
  index 91: expected '2'  vs  actual '7'
  index 92: expected '3'  vs  actual '2'
  index 93: expected '9'  vs  actual '3'
  index 94: expected '8'  vs  actual '9'
  index 95: expected '2'  vs  actual '8'
  index 96: expected '6'  vs  actual '2'
  index 97: expected '2'  vs  actual '6'
  index 98: expected '5'  vs  actual '2'

Copy this exact 99-digit string (the expected value) and paste it into the app input, then Submit:
246451121036528202623890120011222498714684815355211850969748918921930947358058258074789422723982625
```
15. After copying this confirmed 99-digit string, I submitted it into the app and it got accepted.
```
246451121036528202623890120011222498714684815355211850969748918921930947358058258074789422723982625
```
16.The sealed observer screen upon submission displayed the message :  
*You have acquired a brand new Shinsu Stabilizer Crystal!*  
17.Next, I went to the barrier screen , passed it and proceeded to the next room where I clicked on '<flag>' to obtain the flag.  
```
flag: citadel{f33ls_g00d_to_n0t_g3t_d33p_fr13d}
```





