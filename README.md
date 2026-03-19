# SushiJumper
A simple doodle jumper like platformer where you must get to higher ground before you are caught by Duncan the Shark

<img width="3840" height="2160" alt="image" src="https://github.com/user-attachments/assets/990cf512-90bb-4379-95b8-19a7f64675d4" />

Feel free to build and test the game, I always appreciate feedback on how to improve. All Assets in this repo are made by me and are freely available under MIT licence, please note that there are external repos included as submodules that maybe subject to different licencing.


## Building Steps

```
git clone --recurse-submodules https://github.com/JackEverson/SushiJumper.git
cd SushiJumper
cmake -B ./build -S .

#g++ or clang
cmake --build ./build -j

#MSVC on Windows
cmake --build ./build --config Release -j
```
