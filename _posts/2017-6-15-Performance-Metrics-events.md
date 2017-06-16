The native CUDA events can be used to measure the performance of tasks in the stream.

Streams
-----------------------
In CUDA, instructions are executed in-order one after the other, asynchronously. Such sequence of operations are executed within a stream. Operations within a single stream are guaranteed to be executed in order while operations in different streams can be interleaved. Multiple, streams allow operations to be executed synchronously. When no stream in mentioned, "null stream" is used to run the commands.

Events
----------------
Events in CUDA help signal specific activities in a stream. CUDA events can help synchronize between multiple streams and also help measure elapsed time between multiple events. CUDA events can be created using cudaEventCreate() and is of the type cudaEvent_t.

In this example, I have used native cuda events to measure the performance of the Mandelbrot Kernal.

This has been done in the following manner. Events for measuring the performance in terms of time are created in the following manner. timerStart and timerStop events signal the same.

	/*
	* Events to measure kernel performance
	*/
	cudaEvent_t timerStart, timerStop;
	cudaEventCreate(&timerStart);
	cudaEventCreate(&timerStop);


To measure the performance of the kernal, the events can be used in the following manner:

	/*
	 * Kernel launch
	 */
	cudaEventRecord(timerStart);
	mandelbrot<char><<<grid, block>>>(image_device, &width, &height);
	cudaEventRecord(timerStop);

The time can then be calculated by recording the time elapsed between the two events.

	float timeElapsed = 0;
	cudaEventElapsedTime(&timeElapsed, timerStart, timerStop);

Events can also be used to synchronize the operation and has been used in the following manner:

	//Synchronize device with timerStop event
	cudaEventSynchronize(timerStop);

This has to be done before the result is to be copied back to the Host from the device.

The complete implementation can be found [here](https://github.com/STEllAR-GROUP/hpxcl/blob/mandelbrot_events/examples/cuda/mandelbrot/mandelbrotCUDA.cu)