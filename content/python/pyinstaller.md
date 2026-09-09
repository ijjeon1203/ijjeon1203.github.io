pyinstaller --onefile --windowed --icon assets/icon/logo.ico --hidden-import=windows --collect-submodules=windows main.py


pyinstaller --onefile --windowed --icon assets/icon/logo.ico --hidden-import=windows.main_window --collect-submodules=windows main.py


pyinstaller --onedir --windowed --icon assets/icon/logo.ico --hidden-import=windows --hidden-import=windows.main_window --hidden-import=psutil --collect-submodules=windows --collect-all=psutil --paths=. main.py

PyInstaller --clean --onedir --windowed --icon assets/icon/logo.ico --hidden-import=windows   --hidden-import=windows.main_window --hidden-import=psutil --collect-submodules=windows   --collect-all=psutil --paths=. main.py


문제가 결국 pyinstaller 가 설치가 안된게 문제였네 제기랄
- 아 여기 적어 놨구나 

pyinstaller 가 .venv 에 없었 

python 으로 실행시키기 

-- 사이에 딱 한칸만 비우기 

```
 PyInstaller --clean --onefile --windowed --icon assets/icon/logo.ico --hidden-import=windows   --hidden-import=windows.main_window --hidden-import=psutil
 --collect-submodules=windows   --collect-all=psutil --paths=. main.py --add-data C:\Users\digitron\Desktop\workspace\ignition_stabilizer\GUI\system\tool\Spin_Tester.exe;C:\Users\digitron\Desktop\workspace\ignition_stabilizer\GUI\system\tool\
 
PyInstaller --clean --onefile --windowed --icon assets/icon/logo.ico --hidden-import=windows --hidden-import=windows.main_window --hidden-import=psutil --collect-submodules=windows --collect-all=psutil --paths=. main.py --add-data "C:\Users\digitron\Desktop\workspace\ignition_stabilizer\GUI\system\tool\Spin_Tester.exe;C:\Users\digitron\Desktop\workspace\ignition_stabilizer\GUI\system\tool\"

PyInstaller --clean --onefile --windowed --icon assets/icon/logo.ico --hidden-import=windows --hidden-import=windows.main_window --hidden-import=psutil --collect-submodules=windows --collect-all=psutil --paths=. main.py --add-data "C:\Users\digitron\Desktop\workspace\ignition_stabilizer\GUI\system\tool\Spin_Tester.exe;." 

```