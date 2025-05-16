To modify the `/home/BSD.txt` file based on your requirements, follow these steps:

### **Step 1: Delete Lines Containing the Word "following"**
Use `grep` to remove lines containing `"following"` and save the result in `/home/BSD_DELETE.txt`:
```bash
grep -v 'following' /home/BSD.txt > /home/BSD_DELETE.txt
```
- `grep -v` → Excludes lines containing `"following"`
- `>` → Saves the output to `/home/BSD_DELETE.txt`

---

### **Step 2: Replace "the" with "their" Without Altering Substrings**
Use `sed` with word boundaries to ensure only exact matches of `"the"` are replaced:
```bash
sed 's/\bthe\b/their/g' /home/BSD.txt > /home/BSD_REPLACE.txt
```
- `\bthe\b` → Matches **only the whole word** `"the"`
- `s/.../.../g` → Performs the substitution globally
- `>` → Saves the output to `/home/BSD_REPLACE.txt`

---

### **Verification**
Check if changes were applied:
```bash
cat /home/BSD_DELETE.txt
cat /home/BSD_REPLACE.txt
```

This ensures that the modifications follow the compliance requirements correctly. Let me know if you need further refinements! 🚀
