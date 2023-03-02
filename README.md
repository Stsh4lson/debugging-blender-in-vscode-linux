# Blender and Vscode Debugger integration
This is a short guide how to write and debug Blender Python script using more comfy editor like VSCode (or VSCodium or any other IDE with abillity to attach to remote debugger also works).\
I also am using Linux here but it would probably work with any other OS.
![image](https://user-images.githubusercontent.com/32339634/222483677-3bd554df-49e5-48df-a2e5-4c018b136b36.png)

# Setting up python environment
I suggest creating virtual environment using python venv or Conda but it is not required.
Install fake bpy module for autosuggestion. Make sure that you are also using the latest blender version.
```bash
pip install fake-bpy-module-latest
```
If you're using older blender version(here 2.93) use:
```bash
pip install fake-bpy-module-2.93
```
# Installing blender debugger add-on
Download https://github.com/AlansCodeLog/blender-debugger-for-vscode using GitHubs “Download Zip” button and follow instructions on repository.
It is important to check `Settings => Interface => Developer Extras` to see relevant commands under `F3` button.
# Setting up vscode and debugger
- Install python extension to VSCode
- Select Debugger tab and select Create Launch JSON.
- Paste this configuration.
  ```json
  "configurations": [
	  {
		"name": "Attach",	
		"type": "python",	
		"request": "attach",	
			"connect": {	
			"host": "localhost",	
			"port": 5678	// This should be the same as in the blender debugger addon in blender
			}	
		}
	]
	```
# Launching script
1. Start VSCode
2. Open up a terminal in VSCode (you can name it Blender)
3. run blender from it (just type `blender` if you have it in PATH). This will blenders output terminal.
4. In blender, open Text Editor panel and paste the following launch script. Replace `test.py`with your main script name.
   ```python
   import bpy
	import os
	 
	filename = "test.py"
	exec(compile(open(filename).read(), filename, 'exec'))
	```
5. Go back to VSCode and create your main script. Make sure correct interpreter is selected, using `F1 => Python: Select interpreter` and select environment where you installed `fake-bpy-module`.
6. Tu run script in blender, go to blenders window and run script from step 4 using Run Script button. If there is any output from the script, it would show in the “blender” terminal in VSCode.
# Debugging a script
1. Place a breakpoint in the main script in VSCode.
2. In blender, start listening with debugpy using `F3 => Debug: Start Debug Server for VS Code`
3. Quickly launch “Attach” option you created in debug menu in VSCode. 
4. If everything went successful, you should see `Debugger is attached` in debug terminal and “Blender” terminal.
5. Start launch script from within blender, a
# Notes
Thanks to `AlansCodeLog` for creating blender addon.
