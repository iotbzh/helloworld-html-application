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

## Troubleshooting

### `pngquant` does not compile

Building the pngquant dependancy may fail, displaying the message
`pngquant failed to build, make sure that libpng-dev is installed`.

If this error occurs, installing the libpng12 package may help. Under
the "Generic AGL Worker" Docker image, the following command can be
used to install it:
```
wget -q -O /tmp/libpng12.deb http://mirrors.kernel.org/ubuntu/pool/main/libp/libpng/libpng12-0_1.2.54-1ubuntu1_amd64.deb && sudo dpkg -i /tmp/libpng12.deb && rm /tmp/libpng12.deb
```
