| | | |
|:---|:---:|---:|
|[�����][Prev]|[������][Up]|[�����][Next]|

#��������� �����������
� ���, ��� �� �� ���� � ���������� � Vulkan?
+ **�����** �������� ����������� ����������, ������� �������� ����� ��� ��� ������� Vulkan, ������ ��� ��� ��������� ����. ���� ����� ���� ���������, � ������ ����� ����� ����������� �������. ������, ��� ����������� ������� ���� ����� �� �������� ����� ������� ������ (��������, ��� ������, ����� �� ��������� ��� ����� ����������, �������� �/��� ����������). ���� ����� ���� ���������, � ����� ������� ������ ����� ������ ����� ��� ����, ������ ��� ������� ���� Vulkan. ��� �� �����, �� ��������� ��� ���� ���������, ���� �������� ������� ��������� �����. ��� �� �����, ���� ������ �� ��������� �������������� ����������, � ���� ��������� ����� �������, �������, �������� �� �������������� � �������� � �������. � ����������� ���� ������ ������. �� ����� ���������� �� ��������: VK_LAYER_[���_������������]_[��������_����]. ��������� ��� ��������� ����:
  + `VK_LAYER_GOOGLE_unique_objects` � �������� ��� ������� � unique pointer (���������� ���������), � �������������� ��� �������������.
  + `VK_LAYER_LUNARG_api_dump` � ������� ��� ������ �������, �� ��������� � ��������. 
  + `VK_LAYER_LUNARG_device_limits` � ���������, � �� ������� � �� ����������. �.�. �������� ����� ���������� �� ��, ����� ��� ��������������� ������� ����������.
  + `VK_LAYER_LUNARG_core_validation` � ��������� ���� ������������ (descriptor set), ��������� ��������� (pipeline state), ��������� ���������� ����� ������� SPIR-V � ����������� ����������, ��������� ���������� � �������� GPU ������, � ����� � �������� �� �������� � ��������� �������.
  + `VK_LAYER_LUNARG_image` � ��������� ������� ������� � ����� ��������� (render target).
  + `VK_LAYER_LUNARG_object_tracker` � ���������� ������� Vulkan, �������� ����� � ������ ������ ��������.
  + `VK_LAYER_LUNARG_parameter_validation` � ��������� ���������, ������������ � �������.
  + `VK_LAYER_LUNARG_swapchain` � ��������� WSI ���������� swapchain �� ���������� �������������.
  + `VK_LAYER_GOOGLE_threading` � ��������� ���������� ������������� API � ������-�������� ����������.
  + `VK_LAYER_LUNARG_standard_validation` � ����-����, ��� ��������� �������� �������� ��������� ����:
    + `VK_LAYER_GOOGLE_threading`
    + `VK_LAYER_LUNARG_parameter_validation`
    + `VK_LAYER_LUNARG_device_limits`
    + `VK_LAYER_LUNARG_object_tracker`
    + `VK_LAYER_LUNARG_image`
    + `VK_LAYER_LUNARG_core_validation`
    + `VK_LAYER_LUNARG_swapchain`
    + `VK_LAYER_GOOGLE_unique_objects`
  + `VK_LAYER_LUNARG_vktrace` � ����, ������� �� ����� �������� �������. �� ����� ��� ����������� ���������� ����� ������� vktrace. ����� ����� ����� ����� ��������������� �������� vkreplay (��������� �� ���� ����� � ����� �� ��������� ������).
  + `VK_LAYER_RENDERDOC_Capture` � ���� ���� ����� �� ������� �������� �������. ����� ��� ��������� RenderDoc, ������� ������� ������� ���������� ��� ����� �������.
  + `VK_LAYER_NV_optimus` � �������� ���������� NVIDIA Optimus. ~~�������� ������ �������? ���? ��� ������ ����� � ������ �� ���� �� ����������?~~
  + `VK_LAYER_VALVE_steam_overlay` � ���� ��� Steam Overlay. ��� �� �������� � ��� ������? � ���� ��� �����!
+ **����������** � ��� ����������, ������� ������������� �������������� ���������� � Vulkan. ���������� ����� ���� ���������� �������, ��������:
  + WSI � ��������� ����������, � ������� ������� ������������� ����� � ���� ��� �� ����� (Vulkan �� ��������� �� ������������� � ����).
  + Debug Report � ����� ������� ���� callback-�������, ������� ����� ���������� �� ����������� ���� ��� �������� ����������� ���������.
  + [���������� ������������ �� AMD](http://gpuopen.com/unlock-the-rasterizer-with-out-of-order-rasterization/ "������� � ��������") � ������, �������� ������ ��� ����������� *"�������"* ���������. ��� ��� ����� � ��� ��� �������� � ������ ��������� ����� ����.
  + ���������� �� NVIDIA � ��������� GLSL ������� ��������, ��� ���������� � SPIR-V (������ � **�������**, �������� ��� ��� ����������, ����� �������� ������� ���-�� ���������).
  + [���������� �� Khronos Group](https://www.khronos.org/registry/vulkan/specs/1.0-wsi_extensions/xhtml/vkspec.html#_vk_khr_sampler_mirror_clamp_to_edge "���������"), ������� ��������� ��������� ��������, ��� �� UVW ������������ ����� ���� ��������.
  + � ������, ������� �������� ��� �����, � �������� ��� ���.

������, ��������� ���� ����� ������������ ����������, ���� ����� �������� � ������. ��������, ��������� ����������� ���� ����� ������������ ���������� ����������. � ������� � ���� ���������� � ���� ����� ������ �� ���� � ������� � ������� ����������� ���� � ����������� ����������.

## ���������� �����������
������, �� ������ 1.0.13 ������������ ���������� �� instance-���� � device-����. ������� � ������ 1.0.13 ������ ���������� ���, � ��� ���� ��������� �����������, � ��������� ������ � ����������� (deprecated). ������� ��� ����, ����������� � instance ����� �������� � �� �������� �������� (�.�. ����� � �� ����������), ��� �� �����, ������ ���� �� �������, ���� ���� ��������� ���������� ������ API.

#����� ���� � ����������
��� ������ ������������� ��������� Vulkan ��� ����, ����� ����� ��� ��������� ���� � ����������.

## ����� ����
���� Vulkan (� ����� �� ��������) ����� ����� � ������� �������
``` c++
VkResult vkEnumerateInstanceLayerProperties(
	uint32_t*                                   pPropertyCount,
	VkLayerProperties*                          pProperties);
```
� �����, �� ��� ���������� ��� ��� ��������. ������ �������� ����� ���� ��� ����������� � �������(in), ��� � ���������� �� �������(out). � ������ ����� ���� ����������, ���� ������ � ����������� (in).
		
+ `pPropertyCount` � ���������� �������� `VkLayerProperties`, ������� ����� ��������� (in) ��� ���������� ��������� ���� (out).
+ `pProperties` � ��������� ������� ����. ����� ���� `nullptr`.

� �����, ������ ��� ���� ��������� ����������� � �������� ��� � ����������, ��� � � ����������.

��������� �������� ���:
``` c++
typedef struct VkLayerProperties {
	char        layerName[VK_MAX_EXTENSION_NAME_SIZE];
	uint32_t    specVersion;
	uint32_t    implementationVersion;
	char        description[VK_MAX_DESCRIPTION_SIZE];
} VkLayerProperties;
```
+ `layerName` � ��� ����.
+ `specVersion` � ������ Vulkan, ��� ������� ��� ������� ���� ����.
+ `implementationVersion` � ������ ���� (������� unsigned integer, ����������������, ���� ��������� �����-�� ���������).
+ `description` � �������� ���� � UTF-8.

��� ������, ��� ����� ������� � ������� ��� ��������� ����:
``` c++
uint32_t available_instance_layer_count = 0;
res = vkEnumerateInstanceLayerProperties(&available_instance_layer_count, nullptr);
if (res != VK_SUCCESS)
	return;
std::vector<VkLayerProperties> available_instance_layers(available_instance_layer_count);
res = vkEnumerateInstanceLayerProperties(&available_instance_layer_count, available_instance_layers.data());
if (available_instance_layer_count)
{
	std::wcout << L"\n\n���� ����������:\n";
	for (uint32_t i = 0; i < available_instance_layer_count; i++)
	{
		VkLayerProperties &properties = available_instance_layers[i];
		std::cout << properties.layerName << (strlen(properties.layerName) < 24 ? "\t" : "")
		<< (strlen(properties.layerName) < 32 ? "\t" : "")
		<< "\t|" << properties.description << "\n";
	}
}
std::cout << "\n\n";
```
� ������� ����� �����:
```
���� ����������:
VK_LAYER_LUNARG_api_dump                |LunarG debug layer
VK_LAYER_LUNARG_core_validation         |LunarG Validation Layer
VK_LAYER_LUNARG_device_limits           |LunarG Validation Layer
VK_LAYER_LUNARG_image                   |LunarG Validation Layer
VK_LAYER_LUNARG_object_tracker          |LunarG Validation Layer
VK_LAYER_LUNARG_parameter_validation    |LunarG Validation Layer
VK_LAYER_LUNARG_screenshot              |LunarG image capture layer
VK_LAYER_LUNARG_swapchain               |LunarG Validation Layer
VK_LAYER_GOOGLE_threading               |Google Validation Layer
VK_LAYER_GOOGLE_unique_objects          |Google Validation Layer
VK_LAYER_LUNARG_vktrace                 |Vktrace tracing library
VK_LAYER_RENDERDOC_Capture              |Debugging capture layer for RenderDoc
VK_LAYER_NV_optimus                     |NVIDIA Optimus layer
VK_LAYER_VALVE_steam_overlay            |Steam Overlay Layer
VK_LAYER_LUNARG_standard_validation     |LunarG Standard Validation Layer
```
��� ���������� ���������� ������ �������, �� ��� ����������, ��� ��� � ������ ������� � ����� ������ ������:
``` c++
VkResult vkEnumerateDeviceLayerProperties(
	VkPhysicalDevice                            physicalDevice,
	uint32_t*                                   pPropertyCount,
	VkLayerProperties*                          pProperties);
```
+ `physicalDevice` � ���������� ����������. 
+ `pPropertyCount` � ���������� �������� `VkLayerProperties`, ������� ����� ��������� (in) ��� ���������� ��������� ���� (out).
+ `pProperties` � ��������� ������� ����. ����� ���� `nullptr`.
	
##����� ����������
	
��� ���������� ���� ������ �������.
``` c++
VkResult vkEnumerateInstanceExtensionProperties(
	const char*                                 pLayerName,
	uint32_t*                                   pPropertyCount,
	VkExtensionProperties*                      pProperties);
```	
+ `pLayerName` � ��� ����, ��� �������� ����� �������� ����������� ����������. ����� �������� nullptr, ����� ������� ���.
+ `pPropertyCount` � ���������� �������� `VkExtensionProperties`, ������� ����� ��������� (in) ��� ���������� ��������� ���������� (out).
+ `pProperties` � ��������� ������� ����������.

� ������� �� ����, ��� ���������� ���������������� ������ �� ���������.

������, ���� ������� �������� playerName ����� ���������, ����� ���������� ����� ���� ����������. ��������, ��� ������������ ���� �� ������ ���� �������� ������� ������������ ����������.

���� ��������� ����� ���:
``` c++
typedef struct VkExtensionProperties {
	char        extensionName[VK_MAX_EXTENSION_NAME_SIZE];
	uint32_t    specVersion;
} VkExtensionProperties;
```
+ `extensionName` � ��� ����������.
+ `specVersion` � ������ ���������� (������� unsigned integer, ����������������, ���� ��������� �����-�� ���������).

������� �� ��������� ����������:
``` c++
uint32_t available_instance_extension_count = 0;
res = vkEnumerateInstanceExtensionProperties(NULL, &available_instance_extension_count, nullptr);
if (res != VK_SUCCESS)
	return;
std::vector<VkExtensionProperties> available_instance_extensions(available_instance_extension_count);
res = vkEnumerateInstanceExtensionProperties(NULL, &available_instance_extension_count, available_instance_extensions.data());
if (available_instance_extension_count)
{
	//����� �� �����.
	std::wcout << L"\n\n���������� ����������:\n";
	for (uint32_t i = 0; i < available_instance_extensions.size(); i++)
	{
		VkExtensionProperties &properties = available_instance_extensions[i];
		std::cout << properties.extensionName << "\n";
	}
	std::cout << "\n\n";
}
```
� ������� ��� ����� �����:
```
���������� ����������:
VK_KHR_surface
VK_KHR_win32_surface
VK_EXT_debug_report
```
���������� `VK_KHR_win32_surface` � �������������������, ��� ��� � ��� ����� ���� � ������ ���������.

������� ��� ��������� ���������� ����������. ��� �� ����������/deprecated, ��� ��� ���� ����������, ��������������� ������ ��� ����������, � ���� ����������, ��������������� ������ ��� ���������� (���� ����� ���� � �����).
``` c++
VkResult vkEnumerateDeviceExtensionProperties(
	VkPhysicalDevice                            physicalDevice,
	const char*                                 pLayerName,
	uint32_t*                                   pPropertyCount,
	VkExtensionProperties*                      pProperties);
```
+ `physicalDevice` � ���������� ����������. 
+ `pLayerName` � ��� ����, ��� �������� ����� �������� ����������� ����������. ����� �������� nullptr, ����� ������� ���.
+ `pPropertyCount` � ���������� �������� `VkExtensionProperties`, ������� ����� ��������� (in) ��� ���������� ��������� ���������� (out).
+ `pProperties` � ��������� ������� ����������.
		
##��������� ���� � ����������
��� ����� �� ������ ��������� ������ ���� � ���������� � ����-��������� �� ����������. ��� ������ ���������� �������, ������� ����� ������� ����� ���� � ����������:
``` c++
std::vector<const char *> instance_layers;
std::vector<const char *> instance_extensions;

std::vector<const char *> device_layers; //deprecated
std::vector<const char *> device_extensions;
```
������� ����������� ���� � ����������. ����� ��� ����� ���� ����������� �������� `VK_LAYER_LUNARG_standard_validation` � ���������� ���������� `VK_EXT_debug_report`, ��� �������� ���� ���� ����������� ������ VK_EXT_DEBUG_REPORT_EXTENSION_NAME.
``` c++
instance_layers.push_back("VK_LAYER_LUNARG_standard_validation");
instance_extensions.push_back(VK_EXT_DEBUG_REPORT_EXTENSION_NAME);

device_layers = instance_layers; //deprecated
```
�����, ������� ��� ��� ������ � ���������� � ����������:
``` c++
VkInstanceCreateInfo instance_info;
//...
instance_info.enabledLayerCount = instance_layers.size();
instance_info.ppEnabledLayerNames = instance_layers.data();

instance_info.enabledExtensionCount = instance_extensions.size();
instance_info.ppEnabledExtensionNames = instance_extensions.data();
//...
```
� ����� � ���������� �� ����������:
``` c++
VkDeviceCreateInfo device_info;
//...

device_info.enabledLayerCount = device_layers.size();
device_info.ppEnabledLayerNames = device_layers.data();

device_info.enabledExtensionCount = device_extensions.size();
device_info.ppEnabledExtensionNames = device_extensions.data();
//...
```
������. ���� � ���������� ����������. ���� �����-�� �� ��� �� ������, ����� ���� ������ `VK_ERROR_LAYER_NOT_PRESENT` ��� `VK_ERROR_EXTENSION_NOT_PRESENT`.

#���������� ����������

�� ������ �� ��, �� � ��� ������ ���� ��������� ����, ����� ������ � ��� �������� ����������. �������, ����� ������������ ���� api dump ��� ������ � �������/�������� (stdout), �� ��� �� �������� ��������� ������������, ������� ��� ��� ���������� Debug Report. ��� ������, ����� �������� ��� ������ ������� � ������� ���������� ��� ���������� � �������� Callback'��. ��� ������� �� ��������� ����������� �� ���������, ��� ��� � ����� ������ ��� ����� ����� �������� ��������� �� �������. ��� ������ �������� ��� ���������:
``` c++
	PFN_vkCreateDebugReportCallbackEXT fvkCreateDebugReportCallbackEXT = NULL;
	PFN_vkDestroyDebugReportCallbackEXT fvkDestroyDebugReportCallbackEXT = NULL;
```
`PFN_` � Pointer Function, ��������� �� �������. � `f` � ������ ��������� �� ��, ��� ��� fetch-�������, �.�. ���������. ���� ��������� ��� ������, ��� ������ ������ �� ��������� ����. ��������� �� ���� ����� ������:
``` c++
typedef VkResult (VKAPI_PTR *PFN_vkCreateDebugReportCallbackEXT)(VkInstance instance, const VkDebugReportCallbackCreateInfoEXT* pCreateInfo, const VkAllocationCallbacks* pAllocator, VkDebugReportCallbackEXT* pCallback);
typedef void (VKAPI_PTR *PFN_vkDestroyDebugReportCallbackEXT)(VkInstance instance, VkDebugReportCallbackEXT callback, const VkAllocationCallbacks* pAllocator);
typedef void (VKAPI_PTR *PFN_vkDebugReportMessageEXT)(VkInstance instance, VkDebugReportFlagsEXT flags, VkDebugReportObjectTypeEXT objectType, uint64_t object, size_t location, int32_t messageCode, const char* pLayerPrefix, const char* pMessage);
```
����������, �� ��� ��? ����� �����, ����� �������� ������ ���� �������.
``` c++
fvkCreateDebugReportCallbackEXT = (PFN_vkCreateDebugReportCallbackEXT)
	vkGetInstanceProcAddr(instance, "vkCreateDebugReportCallbackEXT");
fvkDestroyDebugReportCallbackEXT = (PFN_vkDestroyDebugReportCallbackEXT)
	vkGetInstanceProcAddr(instance, "vkDestroyDebugReportCallbackEXT");
```	
������� ��������. ������ ���������� ��������� ���������, ������� �������� ���������� � ����� ������� ��������� ������ (callback function):
``` c++
typedef struct VkDebugReportCallbackCreateInfoEXT {
	VkStructureType                 sType;
	const void*                     pNext;
	VkDebugReportFlagsEXT           flags;
	PFN_vkDebugReportCallbackEXT    pfnCallback;
	void*                           pUserData;
} VkDebugReportCallbackCreateInfoEXT;
```
+ `sType` � ��� ��������� , �.�. `VK_STRUCTURE_TYPE_DEBUG_REPORT_CREATE_INFO_EXT`.
+ `pNext` � ������� (`nullptr`).
+ `flags` � ����� ���������, ������� Callback ������� ����� ���������. ��������, ����� �������, ��� ������� ����� ��������� ������ ��������� �� �������.
+ `pfnCallback` � ��������� �� Callback �������.
+ `pUserData` � ������ ���������. ����� �������� `nullptr`, � ����� ���-�� ���������. ���� �� �� `nullptr`, �� ���� ��������� ����� ��������� � callback �������.

��������� � ������:
``` c++
typedef enum VkDebugReportFlagBitsEXT {
	VK_DEBUG_REPORT_INFORMATION_BIT_EXT = 0x00000001,
	VK_DEBUG_REPORT_WARNING_BIT_EXT = 0x00000002,
	VK_DEBUG_REPORT_PERFORMANCE_WARNING_BIT_EXT = 0x00000004,
	VK_DEBUG_REPORT_ERROR_BIT_EXT = 0x00000008,
	VK_DEBUG_REPORT_DEBUG_BIT_EXT = 0x00000010,
} VkDebugReportFlagBitsEXT;
typedef VkFlags VkDebugReportFlagsEXT;
```
+ `VK_DEBUG_REPORT_INFORMATION_BIT_EXT` � ������� �������������� ���������.
+ `VK_DEBUG_REPORT_WARNING_BIT_EXT` � ��������������.
+ `VK_DEBUG_REPORT_PERFORMANCE_WARNING_BIT_EXT` � �������������� � ������������������.
+ `VK_DEBUG_REPORT_ERROR_BIT_EXT` � ������.
+ `VK_DEBUG_REPORT_DEBUG_BIT_EXT` � ���������� ��������� (��������� �� ������ ����������).

������, ��� ����� ���� ��������� � ������� ������� �������� ��������, ��� ��� ���������� �������� ����� ��� ����� ��������� ��������� ������.

������ ���������, ��� ������ ��������� ���� �������:
``` c++
VKAPI_ATTR VkBool32 VKAPI_CALL DebugReportCallback(
	VkDebugReportFlagsEXT flags,
	VkDebugReportObjectTypeEXT objectType,
	uint64_t object,
	size_t location,
	int32_t messageCode,
	const char *pLayerPrefix,
	const char *pMessage,
	void *pUserData)
{
	//..
	return VK_FALSE;
}
```
� ���, ����� ����� `VKAPI_ATTR` � `VKAPI_CALL`? �� ������, ��� ���������� � ������� � ��������� �������. ������� ����� � �� � ������, ���� ��������� ������������� ����. ���� � Windows ������������ ������ ���������� � �������, �� � Linux � ���������.

������������ ��� � ���������� (bool). ���� ������� `VK_TRUE`, �� �������� ������ � ��������� ���� (� � ��������� � ���� Vulkan) ������������. �����������, `VK_FALSE` ����� �������� �������� � ���������� ������ �����������.

�������, ����� ��������� � �������:

+ `flags` � ��� ���� ��������� (������ ����). ��� ����� ���������� ��� ���������, ������� ������.
+ `objectType` � ��� �������, � ������� ���-�� ���������.
+ `object` � ��� ������.
+ `location` � ��������������� �������... ��� � �� � ����� ����� ������� �������� ����� ������������. ������� ����? ����� ������? ��� �����...
+ `messageCode` � ��� ���������.
+ `pLayerPrefix` � ���� (� ������ ��� ������� � ����������� ���), � ������� ������������ ���������.
+ `pMessage` � ���� ���������.
+ `pUserData` � ���������, ������� ��� �� ����� ��������� � ��������� � ����������� � callback'�.

� ���, �� ����������� ����. ����� ����������! ��� ������ ���������� ���� ������� �������� (��� ���������):
``` c++
VkResult vkCreateDebugReportCallbackEXT(
	VkInstance instance,
	const VkDebugReportCallbackCreateInfoEXT* pCreateInfo,
	const VkAllocationCallbacks* pAllocator,
	VkDebugReportCallbackEXT* pCallback);
```	
+ `instance` � ����� ����������, � �������� ���������� callback.
+ `pCreateInfo` � ��������� �� ��������� � ����������� � callback.
+ `pAllocator` � callback'� ��� ���������� �������. ����� ���� `nullptr`.
+ `pCallback` � ������������ ����� ��� callback, ����� ���� ����������� �������� callback (� ����� �� ������ ��).

����������:
``` c++
VkDebugReportCallbackCreateInfoEXT debug_report_callback_info;
memset(&debug_report_callback_info, 0, sizeof(debug_report_callback_info));
debug_report_callback_info.sType = VK_STRUCTURE_TYPE_DEBUG_REPORT_CREATE_INFO_EXT;
debug_report_callback_info.flags = VK_DEBUG_REPORT_DEBUG_BIT_EXT |
	VK_DEBUG_REPORT_INFORMATION_BIT_EXT | VK_DEBUG_REPORT_WARNING_BIT_EXT |
	VK_DEBUG_REPORT_PERFORMANCE_WARNING_BIT_EXT | VK_DEBUG_REPORT_ERROR_BIT_EXT;
debug_report_callback_info.pfnCallback = DebugReportCallback;

VkDebugReportCallbackEXT debug_report_callback = VK_NULL_HANDLE;
res = fvkCreateDebugReportCallbackEXT(instance, &debug_report_callback_info, nullptr, &debug_report_callback);
```
����������� ����� ������� ������ ���. �� ���������� � ������. ���� Callback ���������������� �� ���� Vulkan.
	
����� ��� ��� �� ����� ����� callback, ��� ����� �������� � ��������� �����. ���� ������� ���������� �������� ���:
``` c++
void vkDestroyDebugReportCallbackEXT(
	VkInstance instance,
	VkDebugReportCallbackEXT callback,
	const VkAllocationCallbacks* pAllocator);
```	
+ `instance` � ����� ����������, � �������� �������� callback.
+ `callback` � ����� ���������� ��� �������� callback-�������.
+ `pAllocator` � callback'� ��� ���������� �������. ����� ���� `nullptr`.

�� � ����������� ����� ��������:
``` c++
fvkDestroyDebugReportCallbackEXT(instance, debug_report_callback, nullptr);
```
#����������
����������� ���������� ���������. � ���� ��� �� ����� ������ �������, � ���������� ��� ������ ����� � ���� � ���������� ����������� ���� � Debug Report. ��� ���� ����� � �� �������, �� ������������.

| | | |
|:---|:---:|---:|
|[�����][Prev]|[������][Up]|[�����][Next]|

[� Readme][Readme]

[Up]: ../Readme.md "������"
[Prev]: ../00Device/Tutorial.md "�����"
[Next]: ../02Commands/Tutorial.md "�����"
[Readme]: ./Readme.md "� Readme"