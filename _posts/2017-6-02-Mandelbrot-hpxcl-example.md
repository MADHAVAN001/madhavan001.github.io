The first task is to use HPXCL Cuda and execute the Mandelbrot set example. Mandelbrot set is one of the classic examples which can help utilize the data parallelism in calculating the points. The computation process is extrememly data parallel and my task was to execute this using multiple devices.

The overall task can be split into multiple parts:
1. Split computation into multiple units
2. Retrieve the computed result
3. Stitch multiple images
4. Save the combined image

So, the first part can be achieved by splitting computation between devices by varying the y-coordinate of the computation. The block size was fit to be (16, 16, 1) and grid size of (width / block.x, 1+std::ceil(height / (block.y*numDevices)), 1). Kernal can be launched with the following parameters (char *image, int width, int height, int yStart) where image is of the dimension width * height and the yStart is the start coordinate.

Once the kernal is executed the result is available in the buffer which contains *image. The results from different buffers can be retreived and stitched together. Each pizel in the image is represented by three values of (R,G,B) which are stored as three consecutive array elements. For stiching multiple images, since the values are in the continuous order, they can be appended at the end of the array.

Once the image is stiched, it has to be stored into the file. This is done using libpng library.


Result
-------------------
The result of executing 512 X 512 image in 2 devices running on the Rostam cluster.

![Mandelbrot](https://raw.githubusercontent.com/MADHAVAN001/madhavan001.github.io/master/images/mandelbrot.png)


The result of executing 1024 X 1024 image in 4 devices running on the Rostam cluster.

![Mandelbrot](https://raw.githubusercontent.com/MADHAVAN001/madhavan001.github.io/master/images/SingleDevice.png)