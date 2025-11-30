# Graphics Driver Issues
This page quickly summarizes graphics driver quirks and issues present in GPU drivers by different manufacturers.

**Index**
* [Driver compatibility charts](#driver-compatibility-charts)
* List of driver issues:
  * [AMD (Proprietary)](#amd-proprietary)
  * [Intel (Proprietary)](#intel-proprietary)
  * [NVIDIA (Proprietary)](#nvidia-proprietary)
  * [AMD (Mesa)](#amd-mesa)
  * [Intel (Mesa)](#intel-mesa)
  * [NVIDIA (Mesa)](#nvidia-mesa)
* » [**Hall of Fame (List of fixed issues)**](#hall-of-fame)

---
<br>

## Driver compatibility charts <a name="driver-compatibility-charts"/>

$${\color{red} Unsupported}$$ - The driver supports the hardware, but due to its poor state, we do not support it. <br>
$${\color{yellow} Legacy}$$ - The driver supports the hardware, has reached end-of-life, but we still have legacy support for it. <br>
$${\color{green} Supported}$$ - The driver supports the hardware, is actively updated and supported.

### AMD
<table>
<tr>
  <th>AMD/ATI Radeon</th>
  <th>orca</th>
  <th>oglp</th>
  <th>r600g</th>
  <th>radeonsi</th>
  <th>xgl</th>
  <th>radv</th>
</tr>
<tr>
  <th>HD 5000 to HD 6000</th>
  <td>$${\color{red} Unsupported}$$</td>
  <th>$${\color{gray} X}$$</th>
  <td>$${\color{green} Supported}$$</td>
  <th>$${\color{gray} X}$$</th>
  <th>$${\color{gray} X}$$</th>
  <th>$${\color{gray} X}$$</th>
</tr>
<tr>
  <th>HD 7000</th>
  <td>$${\color{red} Unsupported}$$</td>
  <th>$${\color{gray} X}$$</th>
  <th>$${\color{gray} X}$$</th>
  <td>$${\color{green} Supported}$$</td>
  <th>$${\color{yellow} Legacy}$$</th>
  <th>$${\color{green} Supported}$$</th>
</tr>
<tr>
  <th>RX 200 to RX 300</th>
  <td>$${\color{red} Unsupported}$$</td>
  <th>$${\color{gray} X}$$</th>
  <th>$${\color{gray} X}$$</th>
  <td>$${\color{green} Supported}$$</td>
  <th>$${\color{yellow} Legacy}$$</th>
  <th>$${\color{green} Supported}$$</th>
</tr>
<tr>
  <th>RX 400 to RX 9000</th>
  <td>$${\color{red} Unsupported}$$</td>
  <th>$${\color{green} Supported}$$</th>
  <th>$${\color{gray} X}$$</th>
  <td>$${\color{green} Supported}$$</td>
  <th>$${\color{green} Supported}$$</th>
  <th>$${\color{green} Supported}$$</th>
</tr>
</table>

**Glossary:**
- **orca:** AMD's legacy proprietary OpenGL driver, used on Windows drivers prior to 22.7.1 and older versions of the AMDGPU PRO driver.
- **oglp:** AMD's modern proprietary OpenGL driver, used on Windows drivers starting on 22.7.1 and newer versions of the AMDGPU PRO driver.
- **r600g:** mesa's open-source OpenGL driver for pre HD 7000 hardware.
- **radeonsi:** mesa's open-source OpenGL driver for HD 7000 and newer hardware.
- **xgl:** AMD's proprietary Vulkan driver, used on Windows drivers and amdvlk (now defunct).
- **radv:** mesa's open-source Vulkan driver.

### NVIDIA
<table>
<tr>
  <th>NVIDIA</th>
  <th>libgl</th>
  <th>libvulkan</th>
  <th>nvk</th>
</tr>
<tr>
  <th>Fermi (400/500)</th>
  <td>$${\color{yellow} Legacy}$$</td>
  <th>$${\color{gray} X}$$</th>
  <td>$${\color{gray} X}$$</td>
</tr>
<tr>
  <th>Kepler (600/700)</th>
  <td>$${\color{yellow} Legacy}$$</td>
  <th>$${\color{gray} X}$$</th>
  <td>$${\color{gray} X}$$</td>
</tr>
<tr>
  <th>Maxwell/Pascal (700/900/1000)</th>
  <td>$${\color{yellow} Legacy}$$</td>
  <th>$${\color{green} Supported}$$</th>
  <td>$${\color{red} Unsupported}$$</td>
</tr>
<tr>
  <th>Turing and newer (1600 to 5000)</th>
  <td>$${\color{green} Supported}$$</td>
  <th>$${\color{green} Supported}$$</th>
  <td>$${\color{green} Supported}$$</td>
</tr>
</table>

**Glossary:**
- **libgl:** NVIDIA's proprietary OpenGL driver.
- **libvulkan:** NVIDIA's proprietary Vulkan driver.
- **nvk:** mesa's open-source Vulkan driver for NVIDIA GPUs.

---
<br>

## AMD (Proprietary) <a name="amd-proprietary"/>
**OpenGL**
- _No known problems at this time_

**Vulkan**
- [MSAA with sample shading disabled does not work on NAVI when using Vulkan](https://community.amd.com/t5/opengl-vulkan/msaa-with-sample-shading-disabled-does-not-work-on-navi-when/td-p/425122) <br>
» **Workaround** implemented: **Yes** (automatic) <br>
» **Reported**: Yes <br>
» **Note:** Forcefully enabling sampleRateShading for all pipelines and calculating the minimum ratio works around this problem

- [Regression on amdvlk/adrenalin causing visual corruption and driver crashes on FBO loops](https://github.com/RPCS3/rpcs3/issues/17267) <br>
» **Workaround** implemented: No <br>
» **Reported**: Yes <br>
» **Note:** Disabling the usage of VK_IMAGE_LAYOUT_ATTACHMENT_FEEDBACK_LOOP_OPTIMAL_EXT works around the issue at the cost of violating the Vulkan specification


## Intel (Proprietary) <a name="intel-proprietary"/>
**OpenGL**
- [GLSL compiler is very broken](https://github.com/RPCS3/rpcs3/issues/6199) <br>
» **Workaround** implemented: No <br>
» **Reported**: No <br>
» **Note**: Intel proprietary OpenGL drivers are unsupported by RPCS3 due to their poor state.

- _**Unsupported.** There are likely other issues as well..._

**Vulkan**
- [Driver crashes with VK_ERROR_FRAGMENTATION](https://github.com/RPCS3/rpcs3/issues/17356) <br>
» **Workaround** implemented: No <br>
» **Reported**: No <br>
» **Note**: Intel proprietary Vulkan drivers are unsupported by RPCS3 due to their poor state.

- [Missing `shaderStorageImageMultisample` Vulkan feature support on Intel iGPUs](https://gitlab.freedesktop.org/mesa/mesa/-/issues/6052) <br>
» **Workaround** implemented: **Yes**, Anti-Aliasing (MSAA) will be automatically disabled by RPCS3 <br>
» **Reported**: **Yes**, on 2020-08-03. Feature unsupported by hardware. <br>

- _**Unsupported.** There are likely other issues as well..._


## NVIDIA (Proprietary) <a name="nvidia-proprietary"/>
**OpenGL**
- Floating point precision issues with Nan/Inf values<br>
» **Workaround** implemented: **Yes** (automatic) <br>
» **Note**: This is not a driver bug as it can be considered implementation-defined behavior.

**Vulkan**
- Floating point precision issues with Nan/Inf values<br>
» **Workaround** implemented: **Yes** (automatic) <br>
» **Note**: This is not a driver bug as it can be considered implementation-defined behavior.

- [Unexpectedly slower performance (-25%) when replacing VK_FORMAT_B8G8R8A8_UNORM with VK_FORMAT_R8G8B8A8_UNORM](https://forums.developer.nvidia.com/t/unexpectedly-slower-performance-25-when-replacing-vk-format-b8g8r8a8-unorm-with-vk-format-r8g8b8a8-unorm/158374) <br>
» **Workaround** used: None <br>
» **Reported**: **Yes**, on 2020-10-30. No replies. <br>


## AMD (Mesa) <a name="amd-mesa"/>
**OpenGL**
- _No known problems at this time_

**Vulkan**
- _No known problems at this time_


## Intel (Mesa) <a name="intel-mesa"/>
**OpenGL**
- **crocus** Driver (Legacy hardware): _No known problems at this time._
- **iris** Driver (Modern hardware): _No known problems at this time._

**Vulkan**
- [Missing `shaderStorageImageMultisample` Vulkan feature support on Intel iGPUs](https://gitlab.freedesktop.org/mesa/mesa/-/issues/6052) <br>
» **Workaround** implemented: **Yes**, Anti-Aliasing (MSAA) will be disabled automatically by RPCS3 <br>
» **Reported**: **Yes**, on 2020-08-03. Feature unsupported by hardware. <br>


## NVIDIA (Mesa) <a name="amd-mesa"/>
**Vulkan**
- _No known problems at this time_

---
<br>

# Hall of Fame <a name="hall-of-fame"/>
List of reported graphics driver bugs that are now fixed. We'd like to thank the developers who fixed these!

- **CRITICAL:** [OpenGL no longer renders **any** game on **any** AMD GPU! (Windows)](https://community.amd.com/message/2949336) <br>
» **Affected** drivers: Radeon Software Adrenalin 19.12.1, 19.12.2, 19.12.3, 20.1.1, 20.1.2, 20.1.3 <br>
» **Workaround** used: None, not possible <br>
» **Fixed** on: Radeon Software Adrenalin 20.1.4

- **High:** [AMD RADV driver crash when using ACO due to unusual control flow (Mesa)](https://gitlab.freedesktop.org/mesa/mesa/issues/2557) <br>
» **Affected** drivers: Mesa 20.0.2 and earlier <br>
» **Workaround** used: None, using RADV with LLVM instead of ACO <br>
» **Fixed** on: Mesa 20.0.3

- **High:** Incorrectly rendered Vulkan shaders due to broken SPIR-V optimization on NVIDIA <br>
» **Affected** drivers: NVIDIA Windows 452.06 and earlier, NVIDIA Linux 450.56.06 and earlier <br>
» **Workaround** used: None <br>
» **Fixed** on: NVIDIA Windows 452.28, NVIDIA Linux 450.56.11

- **High:** Driver instability leading to crashes on NVIDIA Windows <br>
» **Affected** drivers: NVIDIA Windows 526.XX <br>
» **Workaround** used: None <br>
» **Fixed** on: NVIDIA Windows 527.37

- **High:** [glMultiDrawArrays is broken on the old AMD OpenGL Windows driver](https://github.com/RPCS3/rpcs3/issues/17711) <br>
» **Affected** drivers: Radeon Software Adrenalin 22.6.1 and older <br>
» **Workaround** used: **Yes** - this seems to be undefined behavior in the spec. The gl_VertexID propagation behavior across MultiDrawArrays is not defined, i.e whether it should continue incrementing of reset to 0 on a new instance. However, due to the comparison with a loop of [first, count] and implied functional equivalence, this may be interpreted as a bug. Either way, RPCS3 provides a workaround using index lookups. <br>
» **Fixed** on: Radeon Software Adrenalin 22.7.1

- **High:** Performance regression on AMD Windows with very high submit and flip latency per frame <br>
» **Affected** drivers: Radeon Software Adrenalin 23.3.2, 23.4.1, 23.4.2 <br>
» **Workaround** used: None <br>
» **Fixed** on: Radeon Software Adrenalin 23.4.3

- **High:** [Graphical corruption on AMD Windows with RDNA3 GPUs when upscaling games](https://github.com/RPCS3/rpcs3/issues/14838) <br>
» **Affected** drivers: Radeon Software Adrenalin 24.1.1 and older <br>
» **Workaround** used: None <br>
» **Fixed** on: Radeon Software Adrenalin 24.2.1

- **High:** Vulkan depth buffer comparison does not work on AMD Windows <br>
» **Affected** drivers: TBD <br>
» **Workaround** used: None <br>
» **Fixed** on: Radeon Software Adrenalin 25.11.1

- **High:** Primitive restart is broken, this is a GCN hardware bug that affects both proprietary and FOSS drivers <br>
» **Affected** drivers: Mesa 18.2.3 and older <br>
» **Workaround** used: **Yes**, [185c2177@rpcs3/rpcs3](https://github.com/RPCS3/rpcs3/pull/4162/commits/185c2177b76c57886efb6daf5c0b155c9f4756e0) (automatic) <br>
» **Fixed** on: Mesa 18.2.4, [eae8f49f@mesa/mesa](https://gitlab.freedesktop.org/mesa/mesa/-/commit/eae8f49fc65e6e625f5e05d38c3bf1b61b84bd3d)

- **Medium:** [Missing `descriptorBindingUniformBufferUpdateAfterBind` support](https://gitlab.freedesktop.org/mesa/mesa/-/issues/5426) <br>
» **Affected** drivers: Mesa 21.2.3 and older <br>
» **Workaround** used: **Yes**, an alternative (slower) code path <br>
» **Fixed** on: Mesa 21.2.4

- **Medium:** [OpenGL's glGetTexImage/glGetTextureImage/glGetTextureImageEXT do not work with immutable textures if pack/unpack byteswap is requested on **any** AMD GPU (Windows)](https://community.amd.com/thread/227876) <br>
» **Affected** drivers: Radeon Software Adrenalin 19.4.2 and earlier <br>
» **Workaround** used: [Manually byteswap texel data](https://github.com/RPCS3/rpcs3/commit/f56a6548b0a7a520301372f8e456c7174b514a68#diff-6067ceb43fa31f7dc9558bdf0b776ad8) (now removed) <br>
» **Fixed** on: Radeon Software Adrenalin 19.4.3

- **Medium:** [Unnecessary implicit subpass dependencies caused performance regression on AMD RADV (Mesa)](https://gitlab.freedesktop.org/mesa/mesa/issues/2502) <br>
» **Affected** drivers: Mesa 20.0.0, 20.0.1 <br>
» **Workaround** used: [Explicitely injecting null subpass dependencies](https://github.com/RPCS3/rpcs3/pull/7909/commits/943cbb1e39fec9cc02ac6193e9b05482c4a36c92#diff-d0082402e2ea9309446e3dc7818f8394) (now removed) <br>
» **Fixed** on: Mesa 20.0.2

- **Medium:** [vkGetQueryPoolResults returns incorrect values when VK_QUERY_RESULT_PARTIAL_BIT is set on NVIDIA (Windows)](https://forums.developer.nvidia.com/t/vkgetquerypoolresults-returns-incorrect-values-when-vk-query-result-partial-bit-is-set/110137) <br>
» **Affected** drivers: NVIDIA GeForce 442.59 and earlier <br>
» **Workaround** used: [Keeping NVIDIA driver from using partial results](https://github.com/RPCS3/rpcs3/pull/7909/commits/c4f539a9cf43e946364a3931f6e5b8c36457d4b4#diff-c9e6fd1ef5ae3e53670d088d2961e556) (now removed) <br>
» **Fixed** on: ~NVIDIA GeForce 442.74

- **Medium:** [Missing `shaderStorageImageMultisample` Vulkan feature support on GCN1 GPUs (RPCS3 crashes if MSAA is enabled)](https://gitlab.freedesktop.org/mesa/mesa/-/issues/2864) <br>
» **Affected** drivers: Mesa 20.0.8 and older <br>
» **Workaround** used: None (disable MSAA on affected drivers) <br>
» **Fixed** on: Mesa 20.1.0

- **Medium:** [Vertex explosion when using ACO shader compiler on AMD RADV (Mesa)](https://gitlab.freedesktop.org/mesa/mesa/-/issues/2848) <br> 
» **Affected** drivers: Mesa 20.2.1 and older <br>
» **Workaround** used: None, not possible. Using the older shader compiler instead of ACO, which was the default prior to Mesa 20.2 <br>
» **Fixed** on: Mesa 20.2.2