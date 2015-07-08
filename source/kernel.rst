Linux Kernel
============

Like we saw for the :ref:`bootloader <bsp_bootloader_label>`, the first thing you need is: sources.
Get them from *Bitbake* build directory (if you built the kernel with it) or get them from the Internet.

*Bitbake* will place the sources under directory:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'kernel_rst-host-171' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="kernel_rst-host-171" class="language-markup">/path/to/build/tmp/work/picozed_zynq7-poky-linux-gnueabi/linux-xlnx/3.14-xilinx+gitAUTOINC+2b48a8aeea-r0</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>


If you are working with the virtual machine, you will find them under directory:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'kernel_rst-host-172' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="kernel_rst-host-172" class="language-markup">/home/architech/architech_sdk/architech/picozed/yocto/build/tmp/work/picozed_zynq7-poky-linux-gnueabi/linux-xlnx/3.14-xilinx+gitAUTOINC+2b48a8aeea-r0</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>


We suggest you to **don't work under Bitbake build directory**, you will pay a speed penalty and you could
have troubles syncronizing the all thing. Just copy them some place else and do what you have to do.

If you didn't build them already with *Bitbake* or you just want to do make every step by hand, you can
always get them from the Internet by cloning the proper repository and checking out the proper hash commit:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'kernel_rst-host-173' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="kernel_rst-host-173" class="language-markup">cd ~/Documents
 git clone -b xlnx_3.14 git://github.com/Xilinx/linux-xlnx.git
 cd linux-xlnx
 git checkout 2b48a8aeea7367359f9eebe55c4a09a05227f32b</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

and by properly patching the sources:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'kernel_rst-host-174' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="kernel_rst-host-174" class="language-markup">patch -p1 &lt; ~/architech_sdk/architech/picozed/yocto/meta-picozed/recipes-kernel/linux/linux-xlnx/3.14/picozed.patch
 patch -p1 &lt; ~/architech_sdk/architech/picozed/yocto/meta-xilinx/recipes-kernel/linux/linux-xlnx/3.14/usb-host-zynq-dr-of-PHY-reset-during-probe.patch
 patch -p1 &lt; ~/architech_sdk/architech/picozed/yocto/meta-xilinx/recipes-kernel/linux/linux-xlnx/3.14/tty-xuartps-Fix-RX-hang-and-TX-corruption-in-set_termios.patch
 cp ~/architech_sdk/architech/picozed/yocto/meta-picozed/recipes-kernel/linux/linux-xlnx/3.14/config .config</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>


If you don't use our SDK then use the following commands to patch the sources:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'kernel_rst-host-175' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="kernel_rst-host-175" class="language-markup">cd ~/Documents
 git clone git://git.yoctoproject.org/meta-xilinx.git
 cd meta-xilinx
 git checkout 2af8d2a0e63aa371045895da03ba2bf98b51adb4</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

Source the script to load the proper evironment for the cross-toolchain (see :ref:`manual_compilation_label` Section) and you are ready to customize and compile the kernel:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'kernel_rst-host-176' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="kernel_rst-host-176" class="language-markup">source ~/architech_sdk/architech/picozed/toolchain/environment-nofs
 LOADADDR=0x0008000 make uImage -j &lt;2 * number of processor's cores&gt;</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

Now you need compile the devicetree file:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'kernel_rst-host-177' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="kernel_rst-host-177" class="language-markup">make picozed-zynq7.dtb</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

By the end of the build process you will get **uImage** and **devicetree** under *arch/arm/boot*.

.. host::

 ~/Documents/linux-xlnx/arch/arm/boot/uImage
 ~/Documents/linux-xlnx/arch/arm/boot/dts/picozed-zynq7.dtb
 

Enjoy!