
# Zephyr RTOS: Introduction

The main question is why – why to develop yet another operating system for embedded devices? Indeed, what it is all for if Wikipedia counts around one hundred of embedded operating systems so that everybody can find one which fits specific application needs in the best way. In this short blog we’ll make attempt to clarify this issue as well as describe main features which distinguish Zephyr OS from other embedded OS.

IoT industry is rapidly developing. There is a long list of boards used as hardware for IoT devices. Sometimes there are cases when different boards are to be used within single application, or a quick switch from one board to the other is demanded. Therefore, a need in a unified platform speeding up development under such circumstances is clearly shaping. Creating such a platform was a driving force of Zephyr OS development. As it is stated at Zephyr official site zephyrproject.org, Zephyr OS is intended to be open, collaborative environment to deliver an open source RTOS, applicable in a wide diversity of use cases, and supporting as many as possible hardware devices, while giving possibilities for upstreaming code and participating in the future roadmap.

A little bit of history. Zephyr originated from the Virtuoso DSP operating system. Later, it was acquired by Wind River Systems in 2015 and renamed to Rocket OS, designed especially for resource-constrained embedded systems. In 2016, Rocket OS transformed into the Zephyr project managed by the Linux Foundation as open source. Since that time Zephyr project is sponsored and contributed mainly by Intel, Nordic Semiconductor, Linaro, Synopsys, Google, NXP, Tencent, Acer, Sony, STMicroelectronics, but also by many others.

Well, now when Zephyr is managed by Linux Foundation the question arises what is the need for Zephyr if Linux kernel itself can do the job well? Indeed, Linux is widely used for IoT applications. However, it requires at least a Cortex-A MCU (or equivalent), and is not the preferred choice for more resource-limited systems, such as Cortex-M [[Ref]](https://www.zephyrproject.org/zephyr-an-operating-system-for-iot).

While Linux vs Zephyr choice for resource-constrained systems is quite obvious, what about comparisons against the other embedded OS? As it was already stated earlier, there are many of them but let’s consider just the most popular ones.

Probably the most powerful embedded OS now is FreeRTOS. It got even more support since being acquired by Amazon in 2017. Being just a bare operating system it intrinsically lacks such things as  device drivers, file systems, crypto modules, network stacks, middleware, and a bootloader. Therefore, they must be added from the other sources. It is rather essential drawback in some use cases.

The other quite popular embedded OS is ARM’s Mbed OS. Specific feature of Mbed OS is that it is compiled on a remote server using the ARMCC C/C++ compiler. However, being provided by ARM, it obviously does not support the other popular IoT platforms.

Apache Mynewt OS is another OS to mention in this context. Mynewt comes with a full implementation of the BLE stack and supports different boards which range, however, is rather limited.

Generally, choice of an embedded OS heavily depends on the specific use case. Therefore, there is no single recipe or single OS of preference to be recommended. Discussion of pros and cons of different OS is out of scope of this blog and focus is made on Zephyr OS specifics and author’s own experience acquired while working with Zephyr OS.
Like many other operating systems, Zephyr provides:

Still, what makes Zephyr OS unique as compared to other OS? Below is the brief list of features.


1. Supported boards
	At the moment this blog is written a number of boards supported by Zephyr was around 170, much more than any another embedded OS has. Why it is important? Because it is very convenient. If due to some reasons decision is made to move to another hardware device the one thing to  do (at least theoretically) is to inform Zephyr compiler which board the code is to be compiled for. Otherwise, without Zephyr or other embedded OS supporting multiple boards, it’s just a start of painful process of getting familiar with board specifics, OS specifics, building toolchain, IDE, etc. Thus, Zephyr essentially reduces time and efforts while moving to another board.
	
2. Scalability
	Zephyr is a highly configurable and modular OS that implements memory protection (even for platforms without an MMU/MPU). It uses Device Tree Support (DTS) only during compile time. Powerful configuration tool allows flexible inclusion of only those features which are really needed in specific application. Memory footprint can be as low as 8k.
	The other specific feature of Zephyr is that it has only one address space. It means that the application code and the kernel are combined in the same binary compilation. 
	
3. Build toolchain
	Being intrinsically cross-platform project, Zephyr naturally uses CMake build system. It also extensively uses command line tool named west. West is used for building, flashing and debugging applications as well as Zephyr repository manager.
	In general, application configuration step is rather complicated in Zephyr. It extensively uses multi-level hierarchical configuration approach. [Here](https://docs.zephyrproject.org/latest/guides/build/index.html) is the link to configuration build overview from official Zephyr documentation page. It will be considered in more details in the next blog. For now, it’s worth stating that it includes Device Tree Compilation step resulting in generation of application specific header files – user need not writing header file manually.
	
4.  Communication interfaces and device drivers
	Zephyr support presently includes Bluetooth, Bluetooth LE 5.0, Ethernet, 802.15.4, Wi-Fi, IPv4/IPv6, 6LoWPAN, Thread, and NFC. 
	
5. Sensor support
	Expectedly, Zephyr has great sensors support with high level of abstraction. The process goes smoothly during enabling sensor which is already supported by Zephyr. List of supported boards and sensors is very rich. However,  if new sensor is to be enabled on a custom board the process turns out to be a little complicated. An issue of implementing new sensor support on Zephyr will be addressed in detail in the next blog.
	
6. Zephyr support and updates.
	Zephyr OS has great SDK and is very well documented. It is permanently developing project and new releases are issued quite frequently. The scope of the project is very wide so that along with rather frequent updates it is a separate task to track all changes and comments. And sometimes application development can stuck for an indefinite while… Author’s personally experienced this when at some time started observing unexpected device resets. Hours were spent for debugging and naturally reasons of the problem were first searched in application code. However, after of couple of debug weeks the reason was localized to be in Bluetooth controller side part. Only at that moment decision was made to update Zephyr to the newest version. And voila – resets magically disappeared and problem was solved.
	
	Nevertheless, general conclusion is that Zephyr OS is very powerful and convenient instrument for embedded application development and is highly recommended for use.
	
	In the next blog an application development process using Zephyr OS will be described in more detail.

