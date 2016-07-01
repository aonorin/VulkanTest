| | |
|:---:|---:|
|[������][Up]|[�����][Next]|

#������: ����������� ����������.
� ���, ��� ������ ��������� � ������������ ���������. ����� ��������� SDK � ��� ����� 3 �����, ������� ���� ����� ���������� ��� ������ ������������ ������ � ���������.
* ����� Include � � ��� ����� ����� ������������ ������.
* ����� Bin � � ��� ����� ����� ��������� (x86_64, �.�. ��� 64 ������ ����������).
* ����� Bin32 � � ��� ����� ����� ��������� (x86, �.�. ��� 32 ������ ����������).

����� �����, ����� ���������� ���� ����������: vulkan-1. �������, ��� Android ���������� ����� ����� ����������� ��� ���������� �����������, �� ��� ���� ��������� ����� � ������ ���������� ��� ����������.

�����, � ����������, ��� ����� �������������� Vulkan, ����� ���������� ������������ ���� *vulkan.h*:
``` c++
#include <vulkan/vulkan.h>
```
��, ������ ����� ���������� � ������.

#�������� ���������� Vulkan. ������ � ��������� �������
##��������� �������
��� ��� ���������� �����, �� ������ �������, ������� �� ����� ������������, ����� ���� �������� � ���������� ����������� ��������. ������� ���� ������� `vkGetInstanceProcAddr`, ������� ����� �������� � ������ �������, ��������� ��������-��������� ������� (��������, `GetProcAddress` ��� *Win32 API*). ���� �������� ����� �������� ��� ��������� �������, ���������� � ����������� � ��� ����. ���������:
``` c++
PFN_vkVoidFunction vkGetInstanceProcAddr(
	VkInstance		instance,
	const char*		pName);
```	
+ `instance` � ��������� Vulkan. ���� ��� �������, ���������� ��� ���� (��������, ������� �������� ����������), ����� ����� ��������� `VK_NULL_HANDLE`.
+ `pName` � ��� �������. ��������, `"vkCreateInstance"`.

��� ������������ ���:
``` c++
typedef void (VKAPI_PTR *PFN_vkVoidFunction)(void);
```	
� �����������, ��� ���� ����� ��������� � ������ ����� ���������� �� �������.

##���������

**���������** (*Instance*) ����� �������� �� ������� `vkCreateInstance`, �� ������, ��� �� ����� � ������������, ����� ��������� ���������� � ���, ����� ������ ���� ��� ���������. � � Vulkan ��� �������� ������ ������� ����� ��������� ����������� ���������.
������ �����, �� ����� ������� ���������� � ����� ����������. ��� ��� �������� ��� ���������:
``` c++
typedef struct VkApplicationInfo {
	VkStructureType sType;
	const void* pNext;
	const char* pApplicationName;
	uint32_t applicationVersion;
	const char* pEngineName;
	uint32_t engineVersion;
	uint32_t apiVersion;
} VkApplicationInfo;
```
� ������ ��������� ������ ���� ��� �����: `sType`, � ����� `pNext`. ��� ��� �� �������:
+ `sType` � ��� ���������. � ����� ������ �� ������ ������� ��� `VK_STRUCTURE_TYPE_APPLICATION_INFO`, ��� �� ������ Vulkan, ����� ������ � ��� ��������� � ����� ���������. ����� ��������� ��������� ���? ����� � ���, ��� ��� Vulkan ���� ����������, � ��������� ������� ����� ��������� ��������� ������� ����. ���� �������� � ����������� �����, ������ �� `VK_STRUCTURE_TYPE_MAX_ENUM = 0x7FFFFFFF`. ����� � ����� ������������� ���� ����������� ��������, ����� ��� `VK_STRUCTURE_TYPE_BEGIN_RANGE`, `VK_STRUCTURE_TYPE_END_RANGE` � `VK_STRUCTURE_TYPE_RANGE_SIZE`.
+ `pNext` � ��������� �� ��������� ���������, ���������� �������������� ���������� �� ����������. � ������ ������ `nullptr`. � �������� ���������� ����� ���� �������, ��� `pNext` � ����������� ��������� ������ ��������� �� ������ ���������, ����������� ��� ����������. � ��� `sType` ����� ������ ���� ��������, �� ��� ������ ���������, ����������� � ����������.
+ `pApplicationName` � ��� ����������, ������� �� ������ �������. � ������ ������ ��� *Null Terminated* (��������� ������ ������ ���� `\0`) *C-������* (��������� �� char). ����� ������� `nullptr`.
+ `applicationVersion` � ������ ����������. ����� ������� `0`.
+ `pEngineName` � ��� ������������� ������ (���� ������� �������), ������� �����, ��� � ��� ����������. ����� ������� `nullptr`.
+ `engineVersion` � ������ ������������� ������. ����� ������� `0`.
+ `apiVersion` � ������ API.

������ � �������. ������ ����� ��� ���������: **�������** (*major*), **��������������** (*minor*) � **����** (*patch*). ��� �������� ������ ���� ������ `VK_MAKE_VERSION(major, minor, patch)`, ������� ��������� ��� ��� ����� � `uint32_t`. ��� ����, ����� �������� ��������� ����� �� ������, ���� ������� `VK_VERSION_MAJOR(version)`, `VK_VERSION_MINOR(version)`, `VK_VERSION_PATCH(version)`. ��� ����� ������� ������ ��� ����������, ������ � ������������� API. � �����, ������ API ����� ������ �� ������ ��������, �� �� ���� ���������� �� �����, ���� ������ ���������� ���� ��������� ������ (patch). ������� ������ ������ ������� `VK_API_VERSION_1_0` (� ���������� SDK � `VK_API_VERSION`).
���� ����� ������ ������������� ����� *vulkan.h*: `VK_HEADER_VERSION`.

������, �������� ���������. ��� ������, � ����� � ���������� ��� ����������:
``` c++
char app_name[] = "Vulkan Tutorian. Device. � GrWolf.";
```
� ����� �������� ��������� ����� �������:
``` c++
VkApplicationInfo app_info;
memset(&app_info, 0, sizeof(app_info));
app_info.sType = VK_STRUCTURE_TYPE_APPLICATION_INFO;
app_info.pApplicationName = app_name;
#ifdef VK_API_VERSION_1_0
app_info.apiVersion = VK_API_VERSION_1_0;
#else
app_info.apiVersion = VK_API_VERSION;
#endif
app_info.applicationVersion = VK_MAKE_VERSION(0, 1, 0);
```
� �����, � �������� � ������ �����, ����� �� ��������� ��� ���� �����. ��� �� �����, ����� ������� ��������� ��������� � ����� �������:
``` c++
VkApplicationInfo app_info = {
	VK_STRUCTURE_TYPE_APPLICATION_INFO,		// VkStructureType 	sType
	nullptr,								// const void 		*pNext
	app_name,								// const char 		*pApplicationName
	VK_MAKE_VERSION(1, 0, 0 ),				// uint32_t 		applicationVersion
	nullptr,								// const char 		*pEngineName
	0,										// uint32_t 		engineVersion
	VK_API_VERSION							// uint32_t 		apiVersion
};
```
������, � �� ��� ��� ������ ��������� �� ���? ����� ����! �� ����� ����, ��������� �������� ����� ���� �������������� ��� ����������� ������ �/��� ����, ����� ���������� �������� ��� �������. � ���, ��� ��� ����������, ������ API ������ �� ��, ����� �� ������ ������� ������������ ����������, � ���� �����, �� ��� ������������. �� �� ���� ���� �����.
������ � ���������, ���������� �� ���������.
``` c++
typedef struct VkInstanceCreateInfo {
	VkStructureType             sType;
	const void*                 pNext;
	VkInstanceCreateFlags       flags;
	const VkApplicationInfo*    pApplicationInfo;
	uint32_t                    enabledLayerCount;
	const char* const*          ppEnabledLayerNames;
	uint32_t                    enabledExtensionCount;
	const char* const*          ppEnabledExtensionNames;
} VkInstanceCreateInfo;
```
���������:
+ `sType` � ��� ���������. � ������ ������ `VK_STRUCTURE_TYPE_INSTANCE_CREATE_INFO`.
+ `pNext` �  ��������� �� ��������� �� ����������, ���� ������� �������. � ������ ������ `nullptr`.
+ `flags` � �����. �� ���� �� ����������, ��������������� ��� �������� �������������. � ������ ������ `0`.
+ `pApplicationInfo` � ��������� �� ���������� � ����������. ����� ������� `nullptr`.

����� ��� ���������� � ����� � �����������, � ������� ����� ��������� � ��������� �����. � ���� `nullptr` � `0`.
���������:
``` c++
VkInstanceCreateInfo instance_info;
memset(&instance_info, 0, sizeof(instance_info));
instance_info.sType = VK_STRUCTURE_TYPE_INSTANCE_CREATE_INFO;
instance_info.pApplicationInfo = &app_info;
```
������ ��������. ����� �������� ���������. ��� ����� ������� �����, ���� �������� ����� ��������.
�������� ����� ���������� � handle'�� � Vulkan. ������ ����� ����� �������� ����� ����������� `VK_DEFINE_HANDLE` ��� `VK_DEFINE_NON_DISPATCHABLE_HANDLE`, ��-�� ���� � ��������� IDE ��������� �������� ����������� (��������, CodeLite, ������� � ������� ��-�� ��� ������ ������). ������� ����� (�.�. ��������� ��� ��������������) ������������ ����� `VK_NULL_HANDLE`. ���� ���� ������� �������� ����� ��� �������:
``` c++
#define VK_DEFINE_HANDLE(object) typedef struct object##_T* object;

#if defined(__LP64__) || defined(_WIN64) || defined(__x86_64__) || defined(_M_X64) || defined(__ia64) || defined (_M_IA64) || defined(__aarch64__) || defined(__powerpc64__)
		#define VK_DEFINE_NON_DISPATCHABLE_HANDLE(object) typedef struct object##_T *object;
#else
		#define VK_DEFINE_NON_DISPATCHABLE_HANDLE(object) typedef uint64_t object;
#endif
```
��� ��� �����, ������ �������������� �� **������������** (*dispatchable*) � **�� ������������** (*non-dispatchable*). ������ ������������ � ������� ��� ������� ������, � ������� �� ��������, ������ �������� � �������� ���������������. ����� ������, ��� ��������� �� ������� ������������ ������, � ������� �� �������, ��� �� ����������� ��������� �� ������������ ������. � ����� ������, ������������� ��������: `VkInstance`, `VkPhysicalDevice`, `VkDevice`, `VkQueue`, `VkCommandBuffer`. ��� ��������� �������� �� �������������.
������� �����:
``` c++
VkInstance instance = VK_NULL_HANDLE;
```
���� �� ����� �������. ������ ���������:
``` c++
VkResult create_instance_result;
```
�� ����� ���������� ����� �������� ���������� ������ ����������. ������ ���������:
``` c++
create_instance_result = vkCreateInstance(&instance_info, nullptr, &instance);
```
������ ��������� ���������� ������� `vkCreateInstance`.
``` c++
VkResult vkCreateInstance(
	const VkInstanceCreateInfo*                 pCreateInfo,
	const VkAllocationCallbacks*                pAllocator,
	VkInstance*                                 pInstance);
```
+ `pCreateInfo` � ��� ��������� �� ����������� ����������� ��������� `VkInstanceCreateInfo`.
+ `pAllocator` � ��������� �� ��������� `VkAllocationCallbacks`, ���������� ������ ������� ���������� �������. ���� ��� ��� �� �����, ����� �������� `nullptr`.
+ `pInstance` � ��������� �� �����, ������� �� ������� ��� �������� ���������� �������.

� ���, ����� ����� ���� ����������?

+ `VK_SUCCESS` � �� ������, �� ����������.
+ `VK_ERROR_OUT_OF_HOST_MEMORY` � �� ������� ������ ����� (����������� ������).
+ `VK_ERROR_OUT_OF_DEVICE_MEMORY` � �� ������� ������ ���������� (�����������).
+ `VK_ERROR_INITIALIZATION_FAILED` � �����, ����������� �������������, ���������� ������.
+ `VK_ERROR_LAYER_NOT_PRESENT` � ��������� ���� �� ����� ���� ��������.
+ `VK_ERROR_EXTENSION_NOT_PRESENT` � ��������� ���������� �� ����� ���� ���������.
+ `VK_ERROR_INCOMPATIBLE_DRIVER` � ������������ �� �������� ����� �������� ��� �� ������� ����. �.�. ��� ��������, ������� �� ����������� �������� ������ `apiVersion` � `VkApplicationInfo` ��� ������� ����������� �����.

����� ������ �������, ����� ��������� ��������� `create_instance_result`. � �������, ����� �������, ��� ��������� ���������� ���� �� ����� �� ������, � �����, ������ ��� ��������� ���������, ����� ��������� � ��� �������� �������.
� ������, � ��������!

#����������, ���������, �������
**����������** � ��� ����������, ����������� �������� � ���������. � Vulkan, � ������� �� ������ API ���� ���������� �� **����������** � **����������** ����������. ������ ��� ������� ���������� ���������, ������� ����� ������������ � ����������, ���������� ������� ��� ���� ����������, �������� ����������� ���������. �������, ��� ������ ����� �������� ������ ���������� ��������� � ������� ������� `vkEnumeratePhysicalDevices`. 

##���������� ����������
���������� ����������� ����� ������� ���������� (���������� GPU), ���������� ����������� ��������� ��� ���-���� ��� (��������� �� ���� ���� ����).
``` c++
VkResult vkEnumeratePhysicalDevices(
	VkInstance                                  instance,
	uint32_t*                                   pPhysicalDeviceCount,
	VkPhysicalDevice*                           pPhysicalDevices);
```	
+ `instance` � ��������� Vulkan.
+ `pPhysicalDeviceCount` � ��������� �� ���������� ���������� ���������.
+ `pPhysicalDevices` � ������ ��������� ���������.

��� ������� ����� ������������ ����� ���������. ������ ������ � ��� �������� ���������� ���������� ���������. ��� ����� ����� `pPhysicalDevices` �������� `VK_NULL_HANDLE`, �� `pPhysicalDeviceCount` ������ ���� �������������� ����������. ���, `*pPhysicalDeviceCount` (�.�. ��������, �� ������� ��������� ���������) ������ ������ ���������� ���������� ���������.

������ ������ � �������� ���� ����������. ����� `pPhysicalDevices` ������ ���� �������������� ���������� �� ������� ������/��������, ������� ����� ��������� ��������, � ����� `*pPhysicalDeviceCount` � ������������ ����������, ������� ����� ������� ������ (� ������, ���� ����������).

������������ ����� ����:
+ `VK_SUCCESS` � �� ������, ��� �������.
+ `VK_INCOMPLETE` � �� ������, �� ���� �������� �� ��� ������ (� ������ ������ � �� ��� ������ ���������� ���������).
+ `VK_ERROR_OUT_OF_HOST_MEMORY` � �� ������� ������ �����.
+ `VK_ERROR_OUT_OF_DEVICE_MEMORY` � �� ������� ������ ����������.
+ `VK_ERROR_INITIALIZATION_FAILED` � �����.

��� ������, ��� ����� �������� ��� ������ ��� ������:
``` c++
uint32_t gpu_count;
if (vkEnumeratePhysicalDevices(instance, &gpu_count, VK_NULL_HANDLE) != VK_SUCCESS)
	return;
std::vector<VkPhysicalDevice> gpu_list(gpu_count);
if (vkEnumeratePhysicalDevices(instance, &gpu_count, gpu_list.data()) != VK_SUCCESS)
	return;
```	
��� ����� ����� ����� ������� ������� ��� ����. ������ ���, ����� ������ ������ ���������� ���������� ��������� � ����������� ��� ������� �����, ������ ���, �������� ��� ���������� ����������.

������, ����� ������ ��� ����������� �� ����������. ���� ��������� �������, ������� ��������� �������� ��� �����������:

+ `vkGetPhysicalDeviceFeatures` � ���������� �������������� ����������.
+ `vkGetPhysicalDeviceFormatProperties` � ���������� �������������� �������.
+ `vkGetPhysicalDeviceImageFormatProperties` � ���������� �������������� ������� �����������.
+ `vkGetPhysicalDeviceProperties` � ���������� �������� ���������� (������� ��������� ����).
+ `vkGetPhysicalDeviceMemoryProperties` � ���������� �������� ������ ����������.
+ `vkGetPhysicalDeviceQueueFamilyProperties` � ���������� �������� �������� �������� ���������� (��������� ����).

��������, ����� ������ ��� ����������, ��� ��� � ������. ��� ����� ���� ������� `vkGetPhysicalDeviceProperties`.
``` c++
void vkGetPhysicalDeviceProperties(
	VkPhysicalDevice				physicalDevice,
	VkPhysicalDeviceProperties*		pProperties);
```
+ `physicalDevice` � ����� ���������� ����������, �������� �������� �� ������ ��������.
+ `pProperties` � ��������� �� ���������, ����������� ��������.

������� �� ���������� ��������, ��� ��� ������ ������ ���������� ���������. ���� ��������� �������� ����� �������:
``` c++
typedef struct VkPhysicalDeviceProperties {
	uint32_t							apiVersion;
	uint32_t							driverVersion;
	uint32_t							vendorID;
	uint32_t							deviceID;
	VkPhysicalDeviceType				deviceType;
	char								deviceName[VK_MAX_PHYSICAL_DEVICE_NAME_SIZE];
	uint8_t								pipelineCacheUUID[VK_UUID_SIZE];
	VkPhysicalDeviceLimits				limits;
	VkPhysicalDeviceSparseProperties	sparseProperties;
} VkPhysicalDeviceProperties;
```	
+ `apiVersion` � ������ API, ������� ������������ ������� ����� ����������. ���������������� ����� �����������, ���������� ����.
+ `driverVersion` � ������ �������� ��� ����� ����������. ���������������� ����� �����������, ���������� ����.
+ `vendorID` � ���������� ������������� ��� vendor'� (��������).
+ `deviceID` � ���������� ������������� ����������.
+ `deviceType` � ��� ����������.
+ `deviceName` � ��� ����������.
+ `pipelineCacheUUID` � ���������� � ������������� �������, ������������ ���������� ����������� ���������� � ��������.
+ `limits` � ������ ����������� ����������. 
+ `sparseProperties` � �������� ����������� ������.

������� ��������� � ��������� ���� ����������:
``` c++
typedef struct VkPhysicalDeviceLimits {
	uint32_t              maxImageDimension1D;
	uint32_t              maxImageDimension2D;
	uint32_t              maxImageDimension3D;
	uint32_t              maxImageDimensionCube;
	uint32_t              maxImageArrayLayers;
	uint32_t              maxTexelBufferElements;
	uint32_t              maxUniformBufferRange;
	uint32_t              maxStorageBufferRange;
	uint32_t              maxPushConstantsSize;
	uint32_t              maxMemoryAllocationCount;
	uint32_t              maxSamplerAllocationCount;
	VkDeviceSize          bufferImageGranularity;
	VkDeviceSize          sparseAddressSpaceSize;
	uint32_t              maxBoundDescriptorSets;
	uint32_t              maxPerStageDescriptorSamplers;
	uint32_t              maxPerStageDescriptorUniformBuffers;
	uint32_t              maxPerStageDescriptorStorageBuffers;
	uint32_t              maxPerStageDescriptorSampledImages;
	uint32_t              maxPerStageDescriptorStorageImages;
	uint32_t              maxPerStageDescriptorInputAttachments;
	uint32_t              maxPerStageResources;
	uint32_t              maxDescriptorSetSamplers;
	uint32_t              maxDescriptorSetUniformBuffers;
	uint32_t              maxDescriptorSetUniformBuffersDynamic;
	uint32_t              maxDescriptorSetStorageBuffers;
	uint32_t              maxDescriptorSetStorageBuffersDynamic;
	uint32_t              maxDescriptorSetSampledImages;
	uint32_t              maxDescriptorSetStorageImages;
	uint32_t              maxDescriptorSetInputAttachments;
	uint32_t              maxVertexInputAttributes;
	uint32_t              maxVertexInputBindings;
	uint32_t              maxVertexInputAttributeOffset;
	uint32_t              maxVertexInputBindingStride;
	uint32_t              maxVertexOutputComponents;
	uint32_t              maxTessellationGenerationLevel;
	uint32_t              maxTessellationPatchSize;
	uint32_t              maxTessellationControlPerVertexInputComponents;
	uint32_t              maxTessellationControlPerVertexOutputComponents;
	uint32_t              maxTessellationControlPerPatchOutputComponents;
	uint32_t              maxTessellationControlTotalOutputComponents;
	uint32_t              maxTessellationEvaluationInputComponents;
	uint32_t              maxTessellationEvaluationOutputComponents;
	uint32_t              maxGeometryShaderInvocations;
	uint32_t              maxGeometryInputComponents;
	uint32_t              maxGeometryOutputComponents;
	uint32_t              maxGeometryOutputVertices;
	uint32_t              maxGeometryTotalOutputComponents;
	uint32_t              maxFragmentInputComponents;
	uint32_t              maxFragmentOutputAttachments;
	uint32_t              maxFragmentDualSrcAttachments;
	uint32_t              maxFragmentCombinedOutputResources;
	uint32_t              maxComputeSharedMemorySize;
	uint32_t              maxComputeWorkGroupCount[3];
	uint32_t              maxComputeWorkGroupInvocations;
	uint32_t              maxComputeWorkGroupSize[3];
	uint32_t              subPixelPrecisionBits;
	uint32_t              subTexelPrecisionBits;
	uint32_t              mipmapPrecisionBits;
	uint32_t              maxDrawIndexedIndexValue;
	uint32_t              maxDrawIndirectCount;
	float                 maxSamplerLodBias;
	float                 maxSamplerAnisotropy;
	uint32_t              maxViewports;
	uint32_t              maxViewportDimensions[2];
	float                 viewportBoundsRange[2];
	uint32_t              viewportSubPixelBits;
	size_t                minMemoryMapAlignment;
	VkDeviceSize          minTexelBufferOffsetAlignment;
	VkDeviceSize          minUniformBufferOffsetAlignment;
	VkDeviceSize          minStorageBufferOffsetAlignment;
	int32_t               minTexelOffset;
	uint32_t              maxTexelOffset;
	int32_t               minTexelGatherOffset;
	uint32_t              maxTexelGatherOffset;
	float                 minInterpolationOffset;
	float                 maxInterpolationOffset;
	uint32_t              subPixelInterpolationOffsetBits;
	uint32_t              maxFramebufferWidth;
	uint32_t              maxFramebufferHeight;
	uint32_t              maxFramebufferLayers;
	VkSampleCountFlags    framebufferColorSampleCounts;
	VkSampleCountFlags    framebufferDepthSampleCounts;
	VkSampleCountFlags    framebufferStencilSampleCounts;
	VkSampleCountFlags    framebufferNoAttachmentsSampleCounts;
	uint32_t              maxColorAttachments;
	VkSampleCountFlags    sampledImageColorSampleCounts;
	VkSampleCountFlags    sampledImageIntegerSampleCounts;
	VkSampleCountFlags    sampledImageDepthSampleCounts;
	VkSampleCountFlags    sampledImageStencilSampleCounts;
	VkSampleCountFlags    storageImageSampleCounts;
	uint32_t              maxSampleMaskWords;
	VkBool32              timestampComputeAndGraphics;
	float                 timestampPeriod;
	uint32_t              maxClipDistances;
	uint32_t              maxCullDistances;
	uint32_t              maxCombinedClipAndCullDistances;
	uint32_t              discreteQueuePriorities;
	float                 pointSizeRange[2];
	float                 lineWidthRange[2];
	float                 pointSizeGranularity;
	float                 lineWidthGranularity;
	VkBool32              strictLines;
	VkBool32              standardSampleLocations;
	VkDeviceSize          optimalBufferCopyOffsetAlignment;
	VkDeviceSize          optimalBufferCopyRowPitchAlignment;
	VkDeviceSize          nonCoherentAtomSize;
} VkPhysicalDeviceLimits;

typedef struct VkPhysicalDeviceSparseProperties {
	VkBool32    residencyStandard2DBlockShape;
	VkBool32    residencyStandard2DMultisampleBlockShape;
	VkBool32    residencyStandard3DBlockShape;
	VkBool32    residencyAlignedMipSize;
	VkBool32    residencyNonResidentStrict;
} VkPhysicalDeviceSparseProperties;
```
������ � ��� ������� �� ������� �������� ������������ Vulkan. � ��� ���������� ��� ���� ���������: 

#��������� ��������
� ���, ��� �� �� ��������� �������� � � ��� �� ����? ����������, ��� ���������� ����� ���������� �� ���������������, ���� ������ �� ��� ����� ��������������. ��������, ���������� ����������� �� 4 ���� ������:
+ *�������* � ���������� ����� �������� 3D/2D �������.
+ *����������* � ���������� ����� ����������� ����������.
+ *�����������* � ���������� ����� ���������� � ���������� ����������.
+ *������ � ����������� �������* � ��� �� ������� ����� ���������� ����������� �����������, �� ��� �� �����, ���� ��������� �����.

��� ��� ����� ���������� � ��������� ���������, ������� ����� ��� �� ����� ��������� �� ��� ���� �����������, ��������� �������. ���� ������� ������������ ����� �����, ���� �������� �������, ����� � ����������� ��� ����� ���� ��������� �����������. �������, ������������� ������������ ���������, �� ����� ���� ������� � �������, ������� �� ������������ ��� ���������. ��������� ����� ��������� ��� ���� ����, ��� � ���. Vulkan ��������� ���������� ��������� � ����������� ����������� � ���� �����. ������ ��������� ����� ����� ������������ ����� ��������.

� �������: NVIDIA GeForce GTX 760 �������� 1 ��������� �������������� ��� �����.  ��������� �������� 16 ��������. ��� ������ � �� ����� ������� ������� NVIDIA.

�������� ���������� � ���������� ����� ��������� �������:
``` c++
void vkGetPhysicalDeviceQueueFamilyProperties(
	VkPhysicalDevice			physicalDevice,
	uint32_t*					pQueueFamilyPropertyCount,
	VkQueueFamilyProperties*	pQueueFamilyProperties);
```
+ `physicalDevice` � ����� ����������� ����������.
+ `pQueueFamilyPropertyCount` � ��������� �� ���������� ��������.
+ `pQueueFamilyProperties` � ���������.

��� �� ��� ����������, ��� ������� �������� �����, ��� � `vkEnumeratePhysicalDevices`. �������, ��� ���� ��������� �������� � `VK_NULL_HANDLE`, �� ������ ������� ���������� ��������, �����, ������ ������� ������� ��������, ������� ������� �� ������. ��������� � ���������:
``` c++
typedef struct VkQueueFamilyProperties {
	VkQueueFlags    queueFlags;
	uint32_t        queueCount;
	uint32_t        timestampValidBits;
	VkExtent3D      minImageTransferGranularity;
} VkQueueFamilyProperties;
```
+ `queueFlags` � ����� ��������� (�������������� ������).
+ `queueCount` � ������������ ���������� ��������.
+ `timestampValidBits` � ����� ��������� ����� ��� `vkCmdWriteTimestamp`, 0 ���� ����� �� ������������.
+ `minImageTransferGranularity` � ����������� "�����������" �������������� ��� ����������� �����������.

���� ����� ������ ����������:

+ `VK_QUEUE_GRAPHICS_BIT` � ������������ �������.
+ `VK_QUEUE_COMPUTE_BIT` � ������������ ����������.
+ `VK_QUEUE_TRANSFER_BIT` � ������������ �����������.
+ `VK_QUEUE_SPARSE_BINDING_BIT` � ������������ ������ � ������������ �������.

� ������� ����� ������������� ���� ����, ������ �� ������� ����������.
``` c++
VkPhysicalDevice gpu = gpu_list[0];
uint32_t family_count = 0;
vkGetPhysicalDeviceQueueFamilyProperties(gpu, &family_count, VK_NULL_HANDLE);
std::vector<VkQueueFamilyProperties> family_properties_list(family_count);
vkGetPhysicalDeviceQueueFamilyProperties(gpu, &family_count, family_properties_list.data());

uint32_t valid_family_index = (uint32_t) -1;
for (uint32_t i = 0; i < family_count; i++) //������� ��� ���������.
{
	VkQueueFamilyProperties &properties = family_properties_list[i];
	if (properties.queueFlags & VK_QUEUE_GRAPHICS_BIT)
	{
		if (valid_family_index == (uint32_t) -1)
			valid_family_index = i;
	}
}
if (valid_family_index == (uint32_t) -1)
	return;
```	
��� ����� ����������, ������������ �� ���������� �� ������� 0 ������� ������, � ����� ���������� ������ ���������, ������� ������������ �������. ��� ��, ��� ����� ����������� ������� ������� �������� (��� ��������� ��� ����������), ������� ����� ���������, ����������, ������������ ����������� ������, � ����� �������� �������� �� ����� (� ���, ��� ��������� ��������� �� ��� ����� � ����� 04).

� ���������� ������� �� �������� `valid_family_index`, ������ �� ����� �����, ��� ����������, � ������ ��� ��������� ������������ �������. ������ ����� ������� ���������� ����������, �� ��� ������ ��� ����� ������� ��� ���� ���������� �� ��������.

#�������

���������� �� ��������, ������� ������ ���� � ����������, Vulkan �������� � ������� ���� ���������:
``` c++
typedef struct VkDeviceQueueCreateInfo {
	VkStructureType             sType;
	const void*                 pNext;
	VkDeviceQueueCreateFlags    flags;
	uint32_t                    queueFamilyIndex;
	uint32_t                    queueCount;
	const float*                pQueuePriorities;
} VkDeviceQueueCreateInfo;
```
+ `sType` � ��� ���������, � ������ ������ `VK_STRUCTURE_TYPE_DEVICE_QUEUE_CREATE_INFO`.
+ `pNext` � `nullptr` ��� ��������� �� ��������� �� ����������.
+ `flags` � ����� ��������������� ��� �������� �������������.
+ `queueFamilyIndex` � ������ ���������, � �������� ����� ������������ �������.
+ `queueCount` � ���������� ��������, ������� ����� ������� � ���� ����������.
+ `pQueuePriorities` � ���������� ��������.

������. �� ������ ������� *����* ������� � ����������, ������� ���� ������� �������� (**`valid_family_index`**):
``` c++
float device_queue_priority[] = {1.0f}; //����������

VkDeviceQueueCreateInfo device_queue_info;
memset(&device_queue_info, 0, sizeof(device_queue_info));
device_queue_info.sType = VK_STRUCTURE_TYPE_DEVICE_QUEUE_CREATE_INFO;

device_queue_info.queueCount = 1;
device_queue_info.queueFamilyIndex = valid_family_index;
device_queue_info.pQueuePriorities = device_queue_priority;
```
**����������** � ��� ������ `float` �������� �� **0.f** (*������� ����������*) �� **1.f** (*������� ����������*). ��� ���� ��������� � ��� ������ ������� ����� ��������� ���� �������.

#����������

��� �������� ����������, ��� ����� ��������� ��������� ���������:
``` c++
typedef struct VkDeviceCreateInfo {
	VkStructureType                    sType;
	const void*                        pNext;
	VkDeviceCreateFlags                flags;
	uint32_t                           queueCreateInfoCount;
	const VkDeviceQueueCreateInfo*     pQueueCreateInfos;
	uint32_t                           enabledLayerCount;
	const char* const*                 ppEnabledLayerNames;
	uint32_t                           enabledExtensionCount;
	const char* const*                 ppEnabledExtensionNames;
	const VkPhysicalDeviceFeatures*    pEnabledFeatures;
} VkDeviceCreateInfo;
```
+ `sType` � ��� ���������, � ������ ������ `VK_STRUCTURE_TYPE_DEVICE_CREATE_INFO`.
+ `pNext` � `nullptr` ��� ��������� �� ��������� �� ����������.
+ `flags` � ����� ��������������� ��� �������� �������������.
+ `queueCreateInfoCount` � ���������� �������� `VkDeviceQueueCreateInfo`, ������� �� ������ ���������.
+ `pQueueCreateInfos` � ��������� `VkDeviceQueueCreateInfo`. ����� �������, ����� ������� ��������� �������� � ������� ����������� (�������, ��� ���� ��������� `VkDeviceQueueCreateInfo` ����� ������� ���� ���� ���������).
+ `pEnabledFeatures` � ���������� ����������. ���� ������ �������� ������ **������** (*required*) � �������� `nullptr`. ��� ��������� ����������� ����� �������� � ������� ������� `vkGetPhysicalDeviceFeatures`.
 
���� � ����������:

+ `enabledLayerCount`
+ `ppEnabledLayerNames`
+ `enabledExtensionCount`
+ `ppEnabledExtensionNames`

������:
``` c++
VkDeviceCreateInfo device_info;
memset(&device_info, 0, sizeof(device_info));
device_info.sType = VK_STRUCTURE_TYPE_DEVICE_CREATE_INFO;
device_info.queueCreateInfoCount = 1;
device_info.pQueueCreateInfos = &device_queue_info;
```
����� ���������� ����� �������. �� ��� �������� ��������� �������:
``` c++
VkResult vkCreateDevice(
	VkPhysicalDevice                            physicalDevice,
	const VkDeviceCreateInfo*                   pCreateInfo,
	const VkAllocationCallbacks*                pAllocator,
	VkDevice*                                   pDevice);
```
+ `physicalDevice` � ���������� ����������, �� ������ �������� �������� ����������.
+ `pCreateInfo` � ���������, ���������� ���������� �� ����������.
+ `pAllocator` � ��������� �� ��������� `VkAllocationCallbacks`, ���������� ������ ������� ���������� �������.
+ `pDevice` � ��������� �� ����� ����������.

������� ���������� ����� ����� �������:
``` c++
VkDevice device = VK_NULL_HANDLE;
if (vkCreateDevice(gpu, &device_info, NULL, &device) != VK_SUCCESS)
	return;
```
� ��� �� ������� `device`. ������, �������, ����� ������ ����� ����.

+ `VK_SUCCESS
+ `VK_ERROR_OUT_OF_HOST_MEMORY
+ `VK_ERROR_OUT_OF_DEVICE_MEMORY
+ `VK_ERROR_INITIALIZATION_FAILED � ����������� ������ ��������� ��� �����.
+ `VK_ERROR_LAYER_NOT_PRESENT
+ `VK_ERROR_EXTENSION_NOT_PRESENT
+ `VK_ERROR_TOO_MANY_OBJECTS � ������ �� �������� **������� ����� ~~�����~~ ��������** (�������� � ��������).
+ `VK_ERROR_DEVICE_LOST � ���������� ~~���������~~ ��������.

##������� ����������

��� ������� ���������� **��������** ��� ����� ����������. ��� ��������, ��� ���������� ������� � ����� ���������� �� ����� ���� ������������ � ������. ��� ����� ������, ��� ���������� �� �������� ���� �� �����, ���� ��������� ����� ���� ����� � ��� �� �����������.

##������� ����������

�������� �������, � �������� �������� ����������, ����� ��� �������:
``` c++
PFN_vkVoidFunction vkGetDeviceProcAddr(
	VkDevice		device,
	const char*		pName);
```	
+ `device` � ����� ����������. �� ����� ���� `VK_NULL_HANDLE`
+ `pName` � ��� �������, ������� �������� � �����������.

##������ ����������

������ ������� �� ������ device lost (������ ����������). ������� ����� DX9, �� ����� ������ ����� ���������� ���� ��� �������� ����, � ������� �� ���-���� ��������, ���� ��� ���� ������ ��������� � ����������. � Vulkan ������ ���������� ����� ���� ���� �� ������ ���� ������:

+ ������ � ����������, �������� ��������� ������ ��������� �� ����������. � ���� ������ ����� ���������� ����������, �� ����� ���� ����� ����� ���������� ��� ��� �������t ������� � �� ������ �� ��� �������������, � ��������� ������� ����� ����� ���������� ������, � ����� ����� ������� ��� �����, ��� � error � device lost. ����� ����� ����� �������� �������� ����������� ���������� ������, � ����� ���������� ������, ���� ��� �� 2 �����.
+ ������������ �/��� ������ ����������� ����������. � ���� ������ ������� ���������� ���������� ������ ������ � ��� ��� ���������� ���������� ��� �� ����� ��������.
+ ������ � �������, ����������� ������. � ���� ������ Vulkan �� ����������� ���������� ���������� ������.

�� ���� ��������� ������� ���������� �������� ���� �� �����.

##������������� ����������

���� ��������, ��� ���������� ������ ������ �� ���������, � ��� ����� ����������, ����� ��������������� ����������� ��������:
``` c++
VkResult vkDeviceWaitIdle(
	VkDevice device);
```
��� ������������ ����� �� ��� ���, ���� ���������� �� �������� ��� ������� �� ���������� ������. ��� ������ ���������, ��� ��� ������� ���������� �����, ������� ����� ���������� �����.

+ `device` � ��� ��� �������, ����� ����������.

���������� ������� ����� ���� �����:

+ `VK_SUCCESS`
+ `VK_ERROR_OUT_OF_HOST_MEMORY`
+ `VK_ERROR_OUT_OF_DEVICE_MEMORY`
+ `VK_ERROR_DEVICE_LOST`

#����������� (cleaning up)

��� ����������� ���������� ����������� ��������� �������:
``` c++
void vkDestroyDevice(
	VkDevice						device,
	const VkAllocationCallbacks*	pAllocator);
```
+ `device` � ����� ����������.
+ `pAllocator` � ��������� �� ��������� `VkAllocationCallbacks`, ���������� ������ ������� ���������� �������.

��� ����������� ����������:
``` c++
void vkDestroyInstance(
	VkInstance						instance,
	const VkAllocationCallbacks*	pAllocator);
```
+ `device` � ����� ����������.
+ `pAllocator` � ��������� �� ��������� `VkAllocationCallbacks`, ���������� ������ ������� ���������� �������.

�� ���� ������ ��������:
``` c++
vkDestroyDevice(device, NULL);
vkDestroyInstance(instance, NULL);
```
#����������

������! ������� ��������, �� ������ ��, ��� ��������. ���� ������ ����� ����� ������� ������.
� �����, ���� ������� �� ����� GDC 2016 ������: "Vulkan API ��������� ������� ����������� ��������. �� �������� � �� ������ �������." ��, Vulkan API ������������� ���������� �� ���� �� DirectX ��� OpenGL, ����, ������� ��, ���� � ��������� ������ �����. �� ��� ���� �� ��� ���������? ��� ����, ����� ����������� �����, ��� � � ����� ���� ���������, ��� ���, � ������, ����� �������������� ������ � "�������" ����� ����������� � �����������. ������ �� ����� ������ ��������� ������ ������� � ����������, � �� ������ ��� �������� �� ����� ������� "������ ��, ������ ���". �� � ������ �������� ���� � Vulkan API ���� ����.

������� �� ��������� �����.
���� �� ������ ���� ����������, ���������� ������ � �.�����: 410012557544062.
�� ��� ������ ��� �� [������](https://money.yandex.ru/to/410012557544062 "������.������").

| | |
|:---:|---:|
|[������][Up]|[�����][Next]|

[� Readme][Readme]

[Up]: ../Readme.md "������"
[Next]: ../01LayersAndExtensions/Tutorial.md "�����"
[Readme]: ./Readme.md "� Readme"