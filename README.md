# Build

Run: 

``` 
git clone --recursive https://github.com/iotbzh/helloworld-html-application
cd helloworld-html-application
npm install     # takes some time on first run
mkdir build
cd build/
cmake ..
make widget
```

Then copy the WGT file onto target (ssh, rsync ...) and install it using:
```
afm-util install <widget file>
```


