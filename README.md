# fn

fn is a simple CLI program written in c++ for Linux to macro shell scripts to aid in workflow automation.
see [run-scripts](https://github.com/Kilthunox/run-scripts) for example automations.



# Compile
Compile from source using g++.
```
g++ src/*.cpp -std=c++17 -o fn
```


# Install
1. Move the newly compiled run executable to where you want the application to live in it's own directory.
```
mv run ~/Applications/fn/fn
```

2. Expose the `fn` directory to `PATH` in the `.bashrc` file.

`~/.bashrc`
```
...
export PATH=$PATH:~/Applications/fn/
```


3. Create a global automation script.
```
cd ~/
mkdir run
cd run
printf "#!/bin/bash \necho $1" > echo.sh
```

4. Restart the terminal.

# Usage
run searches for global scripts first, then local scripts from the working directory override global scripts.
Test if the new echo script was installed by using this script from any directory:
```
run echo HelloWorld
```
-> HelloWorld 


Adding a `run/` directory to the root of your project allows project-specific automations. 

`~/projects/project/run/echo.sh`
```
#!/bin/bash
echo $PWD
```

Test the script from `~/projects/project/.`:
```
fn echo HelloWorld 
```
-> ~/projects/project/

The working directory is printed because the local script has overwritten the global script.

Ensure that all run scripts have a `.sh` file extension. All other files will be ignored.
