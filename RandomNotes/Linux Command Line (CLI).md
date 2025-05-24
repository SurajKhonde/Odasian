Linux में `man` (short for **manual**) एक कमांड है जो किसी भी कमांड, प्रोग्राम, या सिस्टम कॉल का **documentation** (manual page) दिखाती है। यह हर Unix/Linux command के बारे में detail में जानकारी देती है
```bash
man [section] command_name
man ls

```
##  ls
Inside a folder you can list all the files that the folder contains using the ls command
```shell
ls
```
`ls /bin` कमांड Linux में `/bin` (binary) डायरेक्टरी के अंदर मौजूद सभी फाइलों को लिस्ट करता है।
 `/bin` डायरेक्टरी में वे essential command binaries होती हैं जो सिस्टम के लिए बूटिंग के समय और single-user mode में जरूरी होती हैं।
 `ls -al /bin`
 `ls -al /bin` कमांड Linux में `/bin` डायरेक्टरी की सभी फाइलों को **डिटेल में** (long listing format) और **hidden files सहित** लिस्ट करता है।
 #####  फील्ड्स का मतलब:

| Field       | Description                            |
| ----------- | -------------------------------------- |
| `-`         | फाइल का टाइप (`d`=directory, `-`=file) |
| `rwxr-xr-x` | permissions (owner/group/others)       |
| `1`         | hard link count                        |
| `root`      | फाइल का owner                          |
| `root`      | फाइल का group                          |
| `12345`     | फाइल का size (bytes में)               |
| `May 6`     | फाइल को आखिरी बार कब modified किया गया |
| `bash`      | फाइल का नाम                            |
#####  क्यों इस्तेमाल करें `-al`?

- `-a`: hidden files भी दिखाता है (जैसे `.file`)    
- `-l`: फाइल्स का detailed information देता है.
![[Pasted image 20250506231220.png]]

## `cd`
 Once you have a folder, you can move into it using the `cd` command. `cd` means change directory. You invoke it specifying a folder to move into. You can specify a folder name, or an entire path.
#####  Examples with Explanation:

| Command       | What it does                                      |
| ------------- | ------------------------------------------------- |
| `cd`          | Home directory में ले जाता है (जैसे `/home/user`) |
| `cd ~`        | Home directory में जाता है (same as `cd`)         |
| `cd /etc`     | `/etc` directory में जाता है                      |
| `cd ..`       | एक level ऊपर जाता है (parent directory)           |
| `cd ../..`    | दो level ऊपर जाता है                              |
| `cd -`        | पिछली directory में वापस जाता है                  |
| `cd /`        | root directory में जाता है (`/`)                  |
| `cd ./folder` | current directory के अंदर `folder` में जाता है    |
| `cd /var/log` | सीधे absolute path से जाता है                     |
######  Special Symbols:
- `.` = current directory
- `..` = parent directory
- `~` = home directory
- `-` = previous directory
##  `pwd`
Whenever you feel lost in the filesystem, call the `pwd` command to know where you are: `pwd` 
It will print the current folder path.
## `mkdir` (Make Directory)
#### Common Usage Examples:

| Command                         | Explanation                                                 |
| ------------------------------- | ----------------------------------------------------------- |
| `mkdir myfolder`                | एक नया folder `myfolder` बनाएगा                             |
| `mkdir folder1 folder2 folder3` | एक साथ कई directories बनाएगा                                |
| `mkdir -p a/b/c`                | nested directories बनाएगा: पहले `a`, फिर `a/b`, फिर `a/b/c` |
## `rmdir` 
का उपयोग आप खाली folders (directories) को delete करने के लिए करते हैं।
###### याद रखने वाली बात:
- `rmdir` **सिर्फ खाली directories** को ही delete कर सकता है।
- अगर directory के अंदर कोई file या folder है, तो यह error देगा।
##### Single folder delete:
```shell
mkdir fruits
rmdir fruits
```
#####  Multiple folders at once:
```shell
mkdir fruits cars
rmdir fruits cars
```
##### ❗ Error Case:
```shell
mkdir fruits
touch fruits/apple.txt
rmdir fruits
rmdir: failed to remove 'fruits': Directory not empty
```
##### To remove non-empty folder:
```shell
rm -r fruits
```
## `mv`
```shell
mv notes.txt /home/user/Documents/
//Rename a file:
mv oldname.txt newname.txt
//Move and Rename both:
mv file1.txt /home/user/renamed_file.txt
//Move a folder:
mv fruits/ /home/user/

```
## `cp`
- किसी **file या folder को copy** करने के लिए।
- Original file/folder को बिना बदले उसकी **duplicate copy** बनाना।
```shell
cp file1.txt file2.txt
//Copy File to Another Directory:
cp notes.txt /home/user/Documents/
//Copy Folder (Recursive):
cp -r folder1/ folder2/
`-r` = recursive, जिससे पूरे folder का structure और content copy होगा।
```
##  `touch` 
`touch` कमांड का इस्तेमाल **नई empty file बनाने** या **existing file की modified time update करने** के लिए किया जाता है।
```shell
// नया empty file बनाना:
touch apple.txt
//एक से ज्यादा files बनाना:
touch a.txt b.txt c.txt
```
##### File क्यों "open in write mode" नहीं होती?
Linux में `touch` सिर्फ file का metadata (जैसे modified time) update करता है — ये actual file को open या edit नहीं करता।
##### Summary:

|Task|Result|
|---|---|
|`touch file.txt`|Empty file बनती है (या update होती है)|
|`touch file1 file2`|Multiple files बनते हैं या update होते हैं|
|`ls -l file.txt`|File info और last modified date दिखाता है|
## `find` 
```shell
find <path> <options> <conditions>
```
 सभी `.js` files को खोजें (current folder और subfolders में):
 ```shell
 find . -name '*.js'

```
- `.` = current directory
- `-name '*.js'` = सभी `.js` वाले नाम match करें
- **क्यों quotes ('')?** `*` को shell expand करने से रोकने के लिए।
##### सिर्फ "`src`" नाम वाले directories खोजें:
```shell
find . -type d -name src

```
- `-type d` = सिर्फ directories
- `-name src` = नाम बिल्कुल `src` होना चाहिए
##### सिर्फ files खोजें:
```shell
find . -type f -name '*.txt'
```
`-type f` = सिर्फ files
##### Case-insensitive search:
```shell
find . -iname 'readme.md'
```
`-iname` = case insensitive match (README.md, ReadMe.md etc. मिलेंगे)

## `ln` 
Linux में आप किसी file का "shortcut" या "pointer" बना सकते हो – इसे **link** कहते हैं।
##### Types of Links:

| Type                          | Use Case & Notes                              |
| ----------------------------- | --------------------------------------------- |
| **Hard Link**                 | Same file content को दूसरे नाम से access करना |
| **Soft Link (Symbolic Link)** | Shortcut जैसा होता है (दूरी से point करता है) |
###### Hard Link (Default)
```shell
ln <original_file> <link_name>
touch recipes.txt
ln recipes.txt newrecipes.txt
```
- `recipes.txt` और `newrecipes.txt` दोनों एक ही data को share करते हैं।
- अगर आप किसी भी एक को edit करोगे, दोनों में same change दिखेगा।
- अगर `recipes.txt` delete हो जाए, तब भी `newrecipes.txt` काम करता रहेगा।
#####  Hard Link limitations:
- Directory को hard link नहीं कर सकते
- दूसरे filesystem या external disk में hard link नहीं बन सकता.
##### Soft Link (Symbolic Link)
Use `-s` flag:
```bash
ln -s <original_file_or_dir> <link_name>
ln -s recipes.txt shortcut.txt
```
- `shortcut.txt` सिर्फ pointer है `recipes.txt` की ओर
- अगर `recipes.txt` delete हो जाए, `shortcut.txt` broken हो जाएगा 
##### कैसे पहचानें
`ls -l`
- Hard link: दिखने में बिल्कुल original file जैसा
- Soft link: Arrow (`->`) दिखेगा, जिससे पता चलता है वो किस file को point कर रहा है.
##### Summary:

| Link Type | Command               | Works Across Disks? | Works for Directories? | Breaks if Original Deleted? |
| --------- | --------------------- | ------------------- | ---------------------- | --------------------------- |
| Hard Link | `ln file linkname`    | ❌ No                | ❌ No                   | ❌ No (still works)          |
| Soft Link | `ln -s file linkname` | ✅ Yes               | ✅ Yes                  | ✅ Yes (broken link)         |
