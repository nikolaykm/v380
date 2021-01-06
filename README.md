###
Need to install FFMpeg first
###

# v380
Extract h264 from v380 camera where you can use it to feed another application

# Help
```
OPTIONS:
  -u              username         (default admin)
  -p              password
  -addr           camera IP/address
  -mac            camera MAC address
  -id             camera ID
  -port           camera port      (default 8800)
  -retry          Number of connection attempt (default 5)
  --enable-ptz=0  Disable pan-tilt-zoom via keyboard press
  --discover      Discover camera
  -h              Show this help
```

# Usage example
### Connect by IP and feed it to ffplay
`./v380 -u admin -p password -port 8800 -addr 192.168.1.2 | ffplay -vcodec h264 -probesize 32 -formatprobesize 0 -avioflags direct -flags low_delay -i -`
### Connect by id and feed it to ffplay
`./v380 -u admin -p password -port 8800 -id 123456 | ffplay -vcodec h264 -probesize 32 -formatprobesize 0 -avioflags direct -flags low_delay -i -`
### Connect by mac address and feed it to ffmpeg to ffserver
`./v380 -p password -mac 11:22:33:aa:bb:cc | ffmpeg -i - http://localhost:8090/feed1.ffm`
### Feed to gstreamer hosting mjpeg
The http server can be found here: https://gist.github.com/misaelnieto/2409785  
`./v380 -p password -mac 11:22:33:aa:bb:cc | gst-launch-1.0 -v fdsrc ! decodebin ! jpegenc ! multipartmux boundary=spionisto ! tcpclientsink host=127.0.0.1 port=9999
`

### The camera can be discovered by using `--discover` command
`v380 --discover`

# Compiling
Use Visual Studio 2015 or on linux use `make` under v380 subdirectory
