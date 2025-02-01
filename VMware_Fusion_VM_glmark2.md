# VMware Fusion VM glmark2

THE Glmark2 best score was with a Shared Graphics memory of 1024 MB for a VMware Fusion VM. The maximum Memory Object Block (MOB) pages increases when shared memory is increased.

| Shared Memory | Score |
|---------------|-------|
| 256 MB        | 2986  |
| 512 MB        | 3044  |
| 1024 MB       | 3299  |
| 2048 MB       | 3182  |
| 8192 MB       | 3015  |

## 256 MB Shared Graphics Memory

Following results are for an Ubuntu 24.04 Arm VM with 4GB memory and "Accelerate 3d Graphics" enabled and "Shared graphics memory" is 256 MB. Host is MacBook Pro with Apple M1 Pro chip runing Sequoia 15.1.1.

Confirm "Accelerate 3D Graphics".

    $ glxinfo | grep "direct rendering"
    direct rendering: Yes
    
    $ glxinfo | grep "OpenGL renderer string"
    OpenGL renderer string: SVGA3D; build: RELEASE;  LLVM;
    
    $ lsmod | grep vmwgfx
    vmwgfx                450560  5
    drm_ttm_helper         12288  1 vmwgfx
    ttm                   106496  2 vmwgfx,drm_ttm_helper
    
    $ sudo dmesg | grep -i vmwgfx
    [    3.080334] vmwgfx 0000:00:0f.0: [drm] Register MMIO at 0x0x000000003d000000 size is 4096 kiB
    [    3.080339] vmwgfx 0000:00:0f.0: [drm] VRAM at 0x0000000070000000 size is 131072 kiB
    [    3.080344] vmwgfx 0000:00:0f.0: [drm] Running on SVGA version 3.
    [    3.080346] vmwgfx 0000:00:0f.0: [drm] Capabilities: cursor, cursor bypass, alpha cursor, 3D, pitchlock, irq mask, traces, command buffers, command buffers 2, gbobject, dx, hp cmd queue, no bb restriction, cap2 register, 
    [    3.080349] vmwgfx 0000:00:0f.0: [drm] Capabilities2: grow otable, intra surface copy, dx2, gb memsize 2, screendma reg, otable ptdepth2, non ms to ms stretchblt, cursor mob, mshint, cb max size 4mb, dx3, frame type, trace full fb, extra regs, lo staging, 
    [    3.080350] vmwgfx 0000:00:0f.0: [drm] DMA map mode: Caching DMA mappings.
    [    3.080389] vmwgfx 0000:00:0f.0: [drm] Legacy memory limits: VRAM = 4096 kB, FIFO = 256 kB, surface = 524288 kB
    [    3.080390] vmwgfx 0000:00:0f.0: [drm] MOB limits: max mob size = 1048576 kB, max mob pages = 65536
    [    3.080391] vmwgfx 0000:00:0f.0: [drm] Maximum display memory size is 262144 kiB
    [    3.093264] vmwgfx 0000:00:0f.0: [drm] No GMR memory available. Graphics memory resources are very limited.
    [    3.095231] vmwgfx 0000:00:0f.0: [drm] Screen Target display unit initialized
    [    3.097219] vmwgfx 0000:00:0f.0: [drm] Using command buffers with DMA pool.
    [    3.097225] vmwgfx 0000:00:0f.0: [drm] Available shader model: SM_5_1X.
    [    3.098324] [drm] Initialized vmwgfx 2.20.0 20211206 for 0000:00:0f.0 on minor 1
    [    3.098676] vmwgfx 0000:00:0f.0: [drm] fb0: vmwgfxdrmfb frame buffer device

    $ echo $XDG_SESSION_TYPE
    wayland

Run benchmark.

    $ sudo apt install glmark2 -y
    ...
    Note, selecting 'glmark2-x11' instead of 'glmark2'
    ...
    $ glmark2
    =======================================================
        glmark2 2023.01
    =======================================================
        OpenGL Information
        GL_VENDOR:      VMware, Inc.
        GL_RENDERER:    SVGA3D; build: RELEASE;  LLVM;
        GL_VERSION:     4.3 (Compatibility Profile) Mesa 24.0.9-0ubuntu0.3
        Surface Config: buf=32 r=8 g=8 b=8 a=8 depth=24 stencil=0 samples=0
        Surface Size:   800x600 windowed
    =======================================================
    [build] use-vbo=false: FPS: 3073 FrameTime: 0.325 ms
    [build] use-vbo=true: FPS: 3417 FrameTime: 0.293 ms
    [texture] texture-filter=nearest: FPS: 3730 FrameTime: 0.268 ms
    [texture] texture-filter=linear: FPS: 3950 FrameTime: 0.253 ms
    [texture] texture-filter=mipmap: FPS: 3792 FrameTime: 0.264 ms
    [shading] shading=gouraud: FPS: 3551 FrameTime: 0.282 ms
    [shading] shading=blinn-phong-inf: FPS: 3352 FrameTime: 0.298 ms
    [shading] shading=phong: FPS: 3014 FrameTime: 0.332 ms
    [shading] shading=cel: FPS: 3154 FrameTime: 0.317 ms
    [bump] bump-render=high-poly: FPS: 3123 FrameTime: 0.320 ms
    [bump] bump-render=normals: FPS: 3499 FrameTime: 0.286 ms
    [bump] bump-render=height: FPS: 3600 FrameTime: 0.278 ms
    [effect2d] kernel=0,1,0;1,-4,1;0,1,0;: FPS: 3662 FrameTime: 0.273 ms
    [effect2d] kernel=1,1,1,1,1;1,1,1,1,1;1,1,1,1,1;: FPS: 3287 FrameTime: 0.304 ms
    [pulsar] light=false:quads=5:texture=false: FPS: 3830 FrameTime: 0.261 ms
    [desktop] blur-radius=5:effect=blur:passes=1:separable=true:windows=4: FPS: 1543 FrameTime: 0.648 ms
    [desktop] effect=shadow:windows=4: FPS: 2379 FrameTime: 0.420 ms
    [buffer] columns=200:interleave=false:update-dispersion=0.9:update-fraction=0.5:update-method=map: FPS: 1215 FrameTime: 0.824 ms
    [buffer] columns=200:interleave=false:update-dispersion=0.9:update-fraction=0.5:update-method=subdata: FPS: 1200 FrameTime: 0.833 ms
    [buffer] columns=200:interleave=true:update-dispersion=0.9:update-fraction=0.5:update-method=map: FPS: 1257 FrameTime: 0.796 ms
    [ideas] speed=duration: FPS: 1974 FrameTime: 0.507 ms
    [jellyfish] <default>: FPS: 3120 FrameTime: 0.321 ms
    [terrain] <default>: FPS: 926 FrameTime: 1.080 ms
    [shadow] <default>: FPS: 2540 FrameTime: 0.394 ms
    [refract] <default>: FPS: 1312 FrameTime: 0.762 ms
    [conditionals] fragment-steps=0:vertex-steps=0: FPS: 3724 FrameTime: 0.269 ms
    [conditionals] fragment-steps=5:vertex-steps=0: FPS: 3724 FrameTime: 0.269 ms
    [conditionals] fragment-steps=0:vertex-steps=5: FPS: 3689 FrameTime: 0.271 ms
    [function] fragment-complexity=low:fragment-steps=5: FPS: 3649 FrameTime: 0.274 ms
    [function] fragment-complexity=medium:fragment-steps=5: FPS: 3370 FrameTime: 0.297 ms
    [loop] fragment-loop=false:fragment-steps=5:vertex-steps=5: FPS: 3631 FrameTime: 0.275 ms
    [loop] fragment-steps=5:fragment-uniform=false:vertex-steps=5: FPS: 3753 FrameTime: 0.266 ms
    [loop] fragment-steps=5:fragment-uniform=true:vertex-steps=5: FPS: 3554 FrameTime: 0.281 ms
    =======================================================
                                      glmark2 Score: 2986 
    =======================================================
    $ sudo apt remove glmark2
    ...

## 512 MB Shared Graphics Memory

    $ sudo dmesg | grep -i vmwgfx
    [    3.109197] vmwgfx 0000:00:0f.0: [drm] Register MMIO at 0x0x000000003d000000 size is 4096 kiB
    [    3.109203] vmwgfx 0000:00:0f.0: [drm] VRAM at 0x0000000070000000 size is 131072 kiB
    [    3.109208] vmwgfx 0000:00:0f.0: [drm] Running on SVGA version 3.
    [    3.109211] vmwgfx 0000:00:0f.0: [drm] Capabilities: cursor, cursor bypass, alpha cursor, 3D, pitchlock, irq mask, traces, command buffers, command buffers 2, gbobject, dx, hp cmd queue, no bb restriction, cap2 register, 
    [    3.109213] vmwgfx 0000:00:0f.0: [drm] Capabilities2: grow otable, intra surface copy, dx2, gb memsize 2, screendma reg, otable ptdepth2, non ms to ms stretchblt, cursor mob, mshint, cb max size 4mb, dx3, frame type, trace full fb, extra regs, lo staging, 
    [    3.109214] vmwgfx 0000:00:0f.0: [drm] DMA map mode: Caching DMA mappings.
    [    3.109264] vmwgfx 0000:00:0f.0: [drm] Legacy memory limits: VRAM = 4096 kB, FIFO = 256 kB, surface = 524288 kB
    [    3.109265] vmwgfx 0000:00:0f.0: [drm] MOB limits: max mob size = 1048576 kB, max mob pages = 131072
    [    3.109267] vmwgfx 0000:00:0f.0: [drm] Maximum display memory size is 262144 kiB
    [    3.122359] vmwgfx 0000:00:0f.0: [drm] No GMR memory available. Graphics memory resources are very limited.
    [    3.122429] vmwgfx 0000:00:0f.0: [drm] Screen Target display unit initialized
    [    3.125492] vmwgfx 0000:00:0f.0: [drm] Using command buffers with DMA pool.
    [    3.125500] vmwgfx 0000:00:0f.0: [drm] Available shader model: SM_5_1X.
    [    3.125776] [drm] Initialized vmwgfx 2.20.0 20211206 for 0000:00:0f.0 on minor 1
    [    3.126403] vmwgfx 0000:00:0f.0: [drm] fb0: vmwgfxdrmfb frame buffer device

    $ echo $XDG_SESSION_TYPE
    wayland

Run benchmark.

    $ glmark2
    =======================================================
        glmark2 2023.01
    =======================================================
        OpenGL Information
        GL_VENDOR:      VMware, Inc.
        GL_RENDERER:    SVGA3D; build: RELEASE;  LLVM;
        GL_VERSION:     4.3 (Compatibility Profile) Mesa 24.0.9-0ubuntu0.3
        Surface Config: buf=32 r=8 g=8 b=8 a=8 depth=24 stencil=0 samples=0
        Surface Size:   800x600 windowed
    =======================================================
    [build] use-vbo=false: FPS: 3014 FrameTime: 0.332 ms
    [build] use-vbo=true: FPS: 3477 FrameTime: 0.288 ms
    [texture] texture-filter=nearest: FPS: 3836 FrameTime: 0.261 ms
    [texture] texture-filter=linear: FPS: 3903 FrameTime: 0.256 ms
    [texture] texture-filter=mipmap: FPS: 3890 FrameTime: 0.257 ms
    [shading] shading=gouraud: FPS: 3610 FrameTime: 0.277 ms
    [shading] shading=blinn-phong-inf: FPS: 3568 FrameTime: 0.280 ms
    [shading] shading=phong: FPS: 3331 FrameTime: 0.300 ms
    [shading] shading=cel: FPS: 3371 FrameTime: 0.297 ms
    [bump] bump-render=high-poly: FPS: 3069 FrameTime: 0.326 ms
    [bump] bump-render=normals: FPS: 3796 FrameTime: 0.263 ms
    [bump] bump-render=height: FPS: 3590 FrameTime: 0.279 ms
    [effect2d] kernel=0,1,0;1,-4,1;0,1,0;: FPS: 3902 FrameTime: 0.256 ms
    [effect2d] kernel=1,1,1,1,1;1,1,1,1,1;1,1,1,1,1;: FPS: 3396 FrameTime: 0.294 ms
    [pulsar] light=false:quads=5:texture=false: FPS: 3826 FrameTime: 0.261 ms
    [desktop] blur-radius=5:effect=blur:passes=1:separable=true:windows=4: FPS: 1527 FrameTime: 0.655 ms
    [desktop] effect=shadow:windows=4: FPS: 2335 FrameTime: 0.428 ms
    [buffer] columns=200:interleave=false:update-dispersion=0.9:update-fraction=0.5:update-method=map: FPS: 1246 FrameTime: 0.803 ms
    [buffer] columns=200:interleave=false:update-dispersion=0.9:update-fraction=0.5:update-method=subdata: FPS: 1230 FrameTime: 0.813 ms
    [buffer] columns=200:interleave=true:update-dispersion=0.9:update-fraction=0.5:update-method=map: FPS: 1290 FrameTime: 0.775 ms
    [ideas] speed=duration: FPS: 2051 FrameTime: 0.488 ms
    [jellyfish] <default>: FPS: 3109 FrameTime: 0.322 ms
    [terrain] <default>: FPS: 935 FrameTime: 1.070 ms
    [shadow] <default>: FPS: 2480 FrameTime: 0.403 ms
    [refract] <default>: FPS: 1293 FrameTime: 0.774 ms
    [conditionals] fragment-steps=0:vertex-steps=0: FPS: 3734 FrameTime: 0.268 ms
    [conditionals] fragment-steps=5:vertex-steps=0: FPS: 3764 FrameTime: 0.266 ms
    [conditionals] fragment-steps=0:vertex-steps=5: FPS: 3675 FrameTime: 0.272 ms
    [function] fragment-complexity=low:fragment-steps=5: FPS: 3784 FrameTime: 0.264 ms
    [function] fragment-complexity=medium:fragment-steps=5: FPS: 3476 FrameTime: 0.288 ms
    [loop] fragment-loop=false:fragment-steps=5:vertex-steps=5: FPS: 3646 FrameTime: 0.274 ms
    [loop] fragment-steps=5:fragment-uniform=false:vertex-steps=5: FPS: 3701 FrameTime: 0.270 ms
    [loop] fragment-steps=5:fragment-uniform=true:vertex-steps=5: FPS: 3654 FrameTime: 0.274 ms
    =======================================================
                                      glmark2 Score: 3044 
    =======================================================

## 1024 MB Shared Graphics Memory

    $ sudo dmesg | grep -i vmwgfx
    [    3.086922] vmwgfx 0000:00:0f.0: [drm] Register MMIO at 0x0x000000003d000000 size is 4096 kiB
    [    3.086927] vmwgfx 0000:00:0f.0: [drm] VRAM at 0x0000000070000000 size is 131072 kiB
    [    3.086934] vmwgfx 0000:00:0f.0: [drm] Running on SVGA version 3.
    [    3.086937] vmwgfx 0000:00:0f.0: [drm] Capabilities: cursor, cursor bypass, alpha cursor, 3D, pitchlock, irq mask, traces, command buffers, command buffers 2, gbobject, dx, hp cmd queue, no bb restriction, cap2 register, 
    [    3.086939] vmwgfx 0000:00:0f.0: [drm] Capabilities2: grow otable, intra surface copy, dx2, gb memsize 2, screendma reg, otable ptdepth2, non ms to ms stretchblt, cursor mob, mshint, cb max size 4mb, dx3, frame type, trace full fb, extra regs, lo staging, 
    [    3.086940] vmwgfx 0000:00:0f.0: [drm] DMA map mode: Caching DMA mappings.
    [    3.086985] vmwgfx 0000:00:0f.0: [drm] Legacy memory limits: VRAM = 4096 kB, FIFO = 256 kB, surface = 524288 kB
    [    3.086987] vmwgfx 0000:00:0f.0: [drm] MOB limits: max mob size = 1048576 kB, max mob pages = 262144
    [    3.086988] vmwgfx 0000:00:0f.0: [drm] Maximum display memory size is 262144 kiB
    [    3.090250] vmwgfx 0000:00:0f.0: [drm] No GMR memory available. Graphics memory resources are very limited.
    [    3.092760] vmwgfx 0000:00:0f.0: [drm] Screen Target display unit initialized
    [    3.094884] vmwgfx 0000:00:0f.0: [drm] Using command buffers with DMA pool.
    [    3.094889] vmwgfx 0000:00:0f.0: [drm] Available shader model: SM_5_1X.
    [    3.098873] [drm] Initialized vmwgfx 2.20.0 20211206 for 0000:00:0f.0 on minor 1
    [    3.099114] vmwgfx 0000:00:0f.0: [drm] fb0: vmwgfxdrmfb frame buffer device

Run benchmark.

    $ glmark2
    =======================================================
        glmark2 2023.01
    =======================================================
        OpenGL Information
        GL_VENDOR:      VMware, Inc.
        GL_RENDERER:    SVGA3D; build: RELEASE;  LLVM;
        GL_VERSION:     4.3 (Compatibility Profile) Mesa 24.0.9-0ubuntu0.3
        Surface Config: buf=32 r=8 g=8 b=8 a=8 depth=24 stencil=0 samples=0
        Surface Size:   800x600 windowed
    =======================================================
    [build] use-vbo=false: FPS: 3051 FrameTime: 0.328 ms
    [build] use-vbo=true: FPS: 3911 FrameTime: 0.256 ms
    [texture] texture-filter=nearest: FPS: 4238 FrameTime: 0.236 ms
    [texture] texture-filter=linear: FPS: 4106 FrameTime: 0.244 ms
    [texture] texture-filter=mipmap: FPS: 4174 FrameTime: 0.240 ms
    [shading] shading=gouraud: FPS: 3859 FrameTime: 0.259 ms
    [shading] shading=blinn-phong-inf: FPS: 3803 FrameTime: 0.263 ms
    [shading] shading=phong: FPS: 3716 FrameTime: 0.269 ms
    [shading] shading=cel: FPS: 3674 FrameTime: 0.272 ms
    [bump] bump-render=high-poly: FPS: 3283 FrameTime: 0.305 ms
    [bump] bump-render=normals: FPS: 4115 FrameTime: 0.243 ms
    [bump] bump-render=height: FPS: 4011 FrameTime: 0.249 ms
    [effect2d] kernel=0,1,0;1,-4,1;0,1,0;: FPS: 4029 FrameTime: 0.248 ms
    [effect2d] kernel=1,1,1,1,1;1,1,1,1,1;1,1,1,1,1;: FPS: 3495 FrameTime: 0.286 ms
    [pulsar] light=false:quads=5:texture=false: FPS: 4070 FrameTime: 0.246 ms
    [desktop] blur-radius=5:effect=blur:passes=1:separable=true:windows=4: FPS: 1562 FrameTime: 0.641 ms
    [desktop] effect=shadow:windows=4: FPS: 2425 FrameTime: 0.413 ms
    [buffer] columns=200:interleave=false:update-dispersion=0.9:update-fraction=0.5:update-method=map: FPS: 1256 FrameTime: 0.797 ms
    [buffer] columns=200:interleave=false:update-dispersion=0.9:update-fraction=0.5:update-method=subdata: FPS: 1229 FrameTime: 0.814 ms
    [buffer] columns=200:interleave=true:update-dispersion=0.9:update-fraction=0.5:update-method=map: FPS: 1271 FrameTime: 0.787 ms
    [ideas] speed=duration: FPS: 2103 FrameTime: 0.476 ms
    [jellyfish] <default>: FPS: 3117 FrameTime: 0.321 ms
    [terrain] <default>: FPS: 997 FrameTime: 1.004 ms
    [shadow] <default>: FPS: 2602 FrameTime: 0.384 ms
    [refract] <default>: FPS: 1333 FrameTime: 0.751 ms
    [conditionals] fragment-steps=0:vertex-steps=0: FPS: 3960 FrameTime: 0.253 ms
    [conditionals] fragment-steps=5:vertex-steps=0: FPS: 3930 FrameTime: 0.254 ms
    [conditionals] fragment-steps=0:vertex-steps=5: FPS: 3944 FrameTime: 0.254 ms
    [function] fragment-complexity=low:fragment-steps=5: FPS: 3941 FrameTime: 0.254 ms
    [function] fragment-complexity=medium:fragment-steps=5: FPS: 3710 FrameTime: 0.270 ms
    [loop] fragment-loop=false:fragment-steps=5:vertex-steps=5: FPS: 3896 FrameTime: 0.257 ms
    [loop] fragment-steps=5:fragment-uniform=false:vertex-steps=5: FPS: 3952 FrameTime: 0.253 ms
    [loop] fragment-steps=5:fragment-uniform=true:vertex-steps=5: FPS: 3851 FrameTime: 0.260 ms
    =======================================================
                                      glmark2 Score: 3229 
    =======================================================

## 2048 MB Shared Graphics Memory

    $ sudo dmesg | grep -i vmwgfx
    [sudo] password for larry: 
    [    3.083810] vmwgfx 0000:00:0f.0: [drm] Register MMIO at 0x0x000000003d000000 size is 4096 kiB
    [    3.083817] vmwgfx 0000:00:0f.0: [drm] VRAM at 0x0000000070000000 size is 131072 kiB
    [    3.083822] vmwgfx 0000:00:0f.0: [drm] Running on SVGA version 3.
    [    3.083824] vmwgfx 0000:00:0f.0: [drm] Capabilities: cursor, cursor bypass, alpha cursor, 3D, pitchlock, irq mask, traces, command buffers, command buffers 2, gbobject, dx, hp cmd queue, no bb restriction, cap2 register, 
    [    3.083830] vmwgfx 0000:00:0f.0: [drm] Capabilities2: grow otable, intra surface copy, dx2, gb memsize 2, screendma reg, otable ptdepth2, non ms to ms stretchblt, cursor mob, mshint, cb max size 4mb, dx3, frame type, trace full fb, extra regs, lo staging, 
    [    3.083831] vmwgfx 0000:00:0f.0: [drm] DMA map mode: Caching DMA mappings.
    [    3.083868] vmwgfx 0000:00:0f.0: [drm] Legacy memory limits: VRAM = 4096 kB, FIFO = 256 kB, surface = 524288 kB
    [    3.083869] vmwgfx 0000:00:0f.0: [drm] MOB limits: max mob size = 1048576 kB, max mob pages = 524288
    [    3.083870] vmwgfx 0000:00:0f.0: [drm] Maximum display memory size is 262144 kiB
    [    3.086129] vmwgfx 0000:00:0f.0: [drm] No GMR memory available. Graphics memory resources are very limited.
    [    3.088672] vmwgfx 0000:00:0f.0: [drm] Screen Target display unit initialized
    [    3.088932] vmwgfx 0000:00:0f.0: [drm] Using command buffers with DMA pool.
    [    3.088940] vmwgfx 0000:00:0f.0: [drm] Available shader model: SM_5_1X.
    [    3.092013] [drm] Initialized vmwgfx 2.20.0 20211206 for 0000:00:0f.0 on minor 1
    [    3.093493] vmwgfx 0000:00:0f.0: [drm] fb0: vmwgfxdrmfb frame buffer device

Run benchmark.

    $ glmark2
    =======================================================
        glmark2 2023.01
    =======================================================
        OpenGL Information
        GL_VENDOR:      VMware, Inc.
        GL_RENDERER:    SVGA3D; build: RELEASE;  LLVM;
        GL_VERSION:     4.3 (Compatibility Profile) Mesa 24.0.9-0ubuntu0.3
        Surface Config: buf=32 r=8 g=8 b=8 a=8 depth=24 stencil=0 samples=0
        Surface Size:   800x600 windowed
    =======================================================
    [build] use-vbo=false: FPS: 3002 FrameTime: 0.333 ms
    [build] use-vbo=true: FPS: 3913 FrameTime: 0.256 ms
    [texture] texture-filter=nearest: FPS: 4179 FrameTime: 0.239 ms
    [texture] texture-filter=linear: FPS: 4063 FrameTime: 0.246 ms
    [texture] texture-filter=mipmap: FPS: 4090 FrameTime: 0.245 ms
    [shading] shading=gouraud: FPS: 3714 FrameTime: 0.269 ms
    [shading] shading=blinn-phong-inf: FPS: 3724 FrameTime: 0.269 ms
    [shading] shading=phong: FPS: 3652 FrameTime: 0.274 ms
    [shading] shading=cel: FPS: 3561 FrameTime: 0.281 ms
    [bump] bump-render=high-poly: FPS: 3253 FrameTime: 0.307 ms
    [bump] bump-render=normals: FPS: 3977 FrameTime: 0.251 ms
    [bump] bump-render=height: FPS: 3916 FrameTime: 0.255 ms
    [effect2d] kernel=0,1,0;1,-4,1;0,1,0;: FPS: 3911 FrameTime: 0.256 ms
    [effect2d] kernel=1,1,1,1,1;1,1,1,1,1;1,1,1,1,1;: FPS: 3510 FrameTime: 0.285 ms
    [pulsar] light=false:quads=5:texture=false: FPS: 4013 FrameTime: 0.249 ms
    [desktop] blur-radius=5:effect=blur:passes=1:separable=true:windows=4: FPS: 1570 FrameTime: 0.637 ms
    [desktop] effect=shadow:windows=4: FPS: 2387 FrameTime: 0.419 ms
    [buffer] columns=200:interleave=false:update-dispersion=0.9:update-fraction=0.5:update-method=map: FPS: 1271 FrameTime: 0.787 ms
    [buffer] columns=200:interleave=false:update-dispersion=0.9:update-fraction=0.5:update-method=subdata: FPS: 1254 FrameTime: 0.798 ms
    [buffer] columns=200:interleave=true:update-dispersion=0.9:update-fraction=0.5:update-method=map: FPS: 1346 FrameTime: 0.743 ms
    [ideas] speed=duration: FPS: 2121 FrameTime: 0.472 ms
    [jellyfish] <default>: FPS: 3274 FrameTime: 0.305 ms
    [terrain] <default>: FPS: 967 FrameTime: 1.035 ms
    [shadow] <default>: FPS: 2593 FrameTime: 0.386 ms
    [refract] <default>: FPS: 1326 FrameTime: 0.755 ms
    [conditionals] fragment-steps=0:vertex-steps=0: FPS: 3873 FrameTime: 0.258 ms
    [conditionals] fragment-steps=5:vertex-steps=0: FPS: 3832 FrameTime: 0.261 ms
    [conditionals] fragment-steps=0:vertex-steps=5: FPS: 3918 FrameTime: 0.255 ms
    [function] fragment-complexity=low:fragment-steps=5: FPS: 3874 FrameTime: 0.258 ms
    [function] fragment-complexity=medium:fragment-steps=5: FPS: 3524 FrameTime: 0.284 ms
    [loop] fragment-loop=false:fragment-steps=5:vertex-steps=5: FPS: 3675 FrameTime: 0.272 ms
    [loop] fragment-steps=5:fragment-uniform=false:vertex-steps=5: FPS: 3883 FrameTime: 0.258 ms
    [loop] fragment-steps=5:fragment-uniform=true:vertex-steps=5: FPS: 3898 FrameTime: 0.257 ms
    =======================================================
                                      glmark2 Score: 3182 
    =======================================================

## 8192 MB Shared Graphics Memory

    $ sudo dmesg | grep -i vmwgfx
    [   33.444609] vmwgfx 0000:00:0f.0: [drm] Register MMIO at 0x0x000000003d000000 size is 4096 kiB
    [   33.444614] vmwgfx 0000:00:0f.0: [drm] VRAM at 0x0000000070000000 size is 131072 kiB
    [   33.444619] vmwgfx 0000:00:0f.0: [drm] Running on SVGA version 3.
    [   33.444622] vmwgfx 0000:00:0f.0: [drm] Capabilities: cursor, cursor bypass, alpha cursor, 3D, pitchlock, irq mask, traces, command buffers, command buffers 2, gbobject, dx, hp cmd queue, no bb restriction, cap2 register, 
    [   33.444624] vmwgfx 0000:00:0f.0: [drm] Capabilities2: grow otable, intra surface copy, dx2, gb memsize 2, screendma reg, otable ptdepth2, non ms to ms stretchblt, cursor mob, mshint, cb max size 4mb, dx3, frame type, trace full fb, extra regs, lo staging, 
    [   33.444625] vmwgfx 0000:00:0f.0: [drm] DMA map mode: Caching DMA mappings.
    [   33.444666] vmwgfx 0000:00:0f.0: [drm] Legacy memory limits: VRAM = 4096 kB, FIFO = 256 kB, surface = 524288 kB
    [   33.444667] vmwgfx 0000:00:0f.0: [drm] MOB limits: max mob size = 1048576 kB, max mob pages = 2097152
    [   33.444668] vmwgfx 0000:00:0f.0: [drm] Maximum display memory size is 262144 kiB
    [   33.457108] vmwgfx 0000:00:0f.0: [drm] No GMR memory available. Graphics memory resources are very limited.
    [   33.457515] vmwgfx 0000:00:0f.0: [drm] Screen Target display unit initialized
    [   33.459518] vmwgfx 0000:00:0f.0: [drm] Using command buffers with DMA pool.
    [   33.459526] vmwgfx 0000:00:0f.0: [drm] Available shader model: SM_5_1X.
    [   33.462534] [drm] Initialized vmwgfx 2.20.0 20211206 for 0000:00:0f.0 on minor 1
    [   33.463479] vmwgfx 0000:00:0f.0: [drm] fb0: vmwgfxdrmfb frame buffer device

Run benchmark.

    $ glmark2
    =======================================================
        glmark2 2023.01
    =======================================================
        OpenGL Information
        GL_VENDOR:      VMware, Inc.
        GL_RENDERER:    SVGA3D; build: RELEASE;  LLVM;
        GL_VERSION:     4.3 (Compatibility Profile) Mesa 24.0.9-0ubuntu0.3
        Surface Config: buf=32 r=8 g=8 b=8 a=8 depth=24 stencil=0 samples=0
        Surface Size:   800x600 windowed
    =======================================================
    [build] use-vbo=false: FPS: 2256 FrameTime: 0.443 ms
    [build] use-vbo=true: FPS: 3668 FrameTime: 0.273 ms
    [texture] texture-filter=nearest: FPS: 3954 FrameTime: 0.253 ms
    [texture] texture-filter=linear: FPS: 3909 FrameTime: 0.256 ms
    [texture] texture-filter=mipmap: FPS: 3897 FrameTime: 0.257 ms
    [shading] shading=gouraud: FPS: 3596 FrameTime: 0.278 ms
    [shading] shading=blinn-phong-inf: FPS: 3526 FrameTime: 0.284 ms
    [shading] shading=phong: FPS: 3444 FrameTime: 0.290 ms
    [shading] shading=cel: FPS: 3459 FrameTime: 0.289 ms
    [bump] bump-render=high-poly: FPS: 3103 FrameTime: 0.322 ms
    [bump] bump-render=normals: FPS: 3815 FrameTime: 0.262 ms
    [bump] bump-render=height: FPS: 3775 FrameTime: 0.265 ms
    [effect2d] kernel=0,1,0;1,-4,1;0,1,0;: FPS: 3869 FrameTime: 0.259 ms
    [effect2d] kernel=1,1,1,1,1;1,1,1,1,1;1,1,1,1,1;: FPS: 3351 FrameTime: 0.298 ms
    [pulsar] light=false:quads=5:texture=false: FPS: 3760 FrameTime: 0.266 ms
    [desktop] blur-radius=5:effect=blur:passes=1:separable=true:windows=4: FPS: 1497 FrameTime: 0.668 ms
    [desktop] effect=shadow:windows=4: FPS: 2278 FrameTime: 0.439 ms
    [buffer] columns=200:interleave=false:update-dispersion=0.9:update-fraction=0.5:update-method=map: FPS: 1228 FrameTime: 0.814 ms
    [buffer] columns=200:interleave=false:update-dispersion=0.9:update-fraction=0.5:update-method=subdata: FPS: 1203 FrameTime: 0.831 ms
    [buffer] columns=200:interleave=true:update-dispersion=0.9:update-fraction=0.5:update-method=map: FPS: 1269 FrameTime: 0.788 ms
    [ideas] speed=duration: FPS: 2027 FrameTime: 0.493 ms
    [jellyfish] <default>: FPS: 3071 FrameTime: 0.326 ms
    [terrain] <default>: FPS: 916 FrameTime: 1.093 ms
    [shadow] <default>: FPS: 2420 FrameTime: 0.413 ms
    [refract] <default>: FPS: 1268 FrameTime: 0.789 ms
    [conditionals] fragment-steps=0:vertex-steps=0: FPS: 3773 FrameTime: 0.265 ms
    [conditionals] fragment-steps=5:vertex-steps=0: FPS: 3628 FrameTime: 0.276 ms
    [conditionals] fragment-steps=0:vertex-steps=5: FPS: 3677 FrameTime: 0.272 ms
    [function] fragment-complexity=low:fragment-steps=5: FPS: 3671 FrameTime: 0.272 ms
    [function] fragment-complexity=medium:fragment-steps=5: FPS: 3425 FrameTime: 0.292 ms
    [loop] fragment-loop=false:fragment-steps=5:vertex-steps=5: FPS: 3424 FrameTime: 0.292 ms
    [loop] fragment-steps=5:fragment-uniform=false:vertex-steps=5: FPS: 3708 FrameTime: 0.270 ms
    [loop] fragment-steps=5:fragment-uniform=true:vertex-steps=5: FPS: 3683 FrameTime: 0.272 ms
    =======================================================
                                      glmark2 Score: 3015 
    =======================================================

## Cleanup

    sudo apt remove glmark2-x11