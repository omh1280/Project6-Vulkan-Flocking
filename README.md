Vulkan Flocking: compute and shading in one pipeline!
======================

**University of Pennsylvania, CIS 565: GPU Programming and Architecture, Project 6**

* Ottavio Hartman
  Windows 10, Fx-8320 @ 3.50GHz 8GB, GTX 1060 3GB

### Vulkan Flocking

  ![](giphy.gif)

This is an implementation of the boids flocking algorithm similar to [here](https://github.com/omh1280/Project1-CUDA-Flocking), except using 
Vulkan.

### Questions

* Why do you think Vulkan expects explicit descriptors for things like generating pipelines and commands? HINT: this may relate to something in the comments about some components using pre-allocated GPU memory.
  * Things like command buffers, which live in GPU memory, can be optimized by the GPU if detailed information about their state is given. The command pool
  (which also lives in GPU memory), takes certain input flags to describe the nature of the commands it will be holding in order to increase potential GPU optimization.

* Describe a situation besides flip-flop buffers in which you may need multiple descriptor sets to fit one descriptor layout.
  * Having multiple descriptor sets could be useful if descriptors change between sets of objects. This means that descriptors associated with some objects
  could be seperate from other objects through the rebinding of descriptor sets.

* What are some problems to keep in mind when using multiple Vulkan queues?
  * Vulkan queues are basically abstractions of multithreading on the GPU. In other words, they give the programmer a way to use GPU power when there may be some tasks
  which are taking a long time. As with any multithreading, the problems such as race conditions need to be taken into account. If the same buffer is used across commands
  in a queue, and those commands run simultaneously, then the data in the buffer is not atomic and could have unexpected bugs.

* What is one advantage of using compute commands that can share data with a rendering pipeline?
  * One advantage is the extremely fast rendering of data. For example, sharing the vertex positions and velocities between the compute and 
  rendering pipelines allows for efficient rendering of the data, since the data does not need to be copied.

### Credits

* [Vulkan examples and demos](https://github.com/SaschaWillems/Vulkan) by [@SaschaWillems](https://github.com/SaschaWillems)
