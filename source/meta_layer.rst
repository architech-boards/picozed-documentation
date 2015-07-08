Meta Layer
==========

A Yocto/OpenEmbedded meta-layer is a directory that contains recipes, configuration files, patches, etc., all needed by
*Bitbake* to properly "see" and build a BSP, a distribution, a (set of) package(s), whatever.
**meta-xilinx** is a meta-layer which defines the BSP for Microzed device, Picozed included. 
You can get it with *git*:

.. raw:: html

 <div>
 <div><b class="admonition-host">&nbsp;&nbsp;Host&nbsp;&nbsp;</b>&nbsp;&nbsp;<a style="float: right;" href="javascript:select_text( 'meta_layer_rst-host-191' );">select</a></div>
 <pre class="line-numbers pre-replacer" data-start="1"><code id="meta_layer_rst-host-191" class="language-markup">git clone -b dizzy https://github.com/architech-boards/meta-microzed.git</code></pre>
 <script src="_static/prism.js"></script>
 <script src="_static/select_text.js"></script>
 </div>

This layer depends with this one which defines the BSP for Xilinx devices:

 | git clone git://git.yoctoproject.org/meta-xilinx.git
 | cd meta-xilinx/
 | git checkout 2af8d2a0e63aa371045895da03ba2bf98b51adb4

Please, refer to the *README* file contained inside the meta-layer directory.

The machine name corresponding to Picozed is **picozed-zynq7**.