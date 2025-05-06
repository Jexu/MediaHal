## Adaptor
This is top adaptor including some public interface for uplayer caller integration.
Caller should init adaptor firstly with struct HalSetting, pass execution params with struct HalParam, and retrieve execution result with struct HalStatus.

## PkgMgr.cpp
This is 2nd layer under Adaptor to pass call requirement from adaptor to internal calling for GPU execution. Could inherit from StatusMgr.

## StatusMgr.cpp
This is parallel layer as PkgMgr for GPU execution status management, caller could retrieve result from this layer async.

## ItfMgr.cpp
This is hw interface management which may contains different sub-hw interface like miIff, mfxItf. For pkgMgr preparing hw cmd instruction for different hw engine.

## ResMgr.cpp
This is hw resource management for MOS_RESOURCE, MOS_SURFACE and MOS_BUFFER allocation, free, sync, lock and unlock.

### reference osInterface
```cpp
typedef struct _MOS_INTERFACE
    MOS_STATUS (* pfnAllocateResource) (
        PMOS_INTERFACE              pOsInterface,
        PMOS_ALLOC_GFXRES_PARAMS    pParams,
        PMOS_RESOURCE               pOsResource);
        
    MOS_STATUS (* pfnFillResource) (
        PMOS_INTERFACE              pOsInterface,
        PMOS_RESOURCE               pResource,
        uint32_t                    dwSize,
        uint8_t                     iValue);
        
    MOS_STATUS (* pfnGetResourceInfo) (
        PMOS_INTERFACE              pOsInterface,
        PMOS_RESOURCE               pOsResource,
        PMOS_SURFACE                pDetails);
        
    void (* pfnFreeResource) (
        PMOS_INTERFACE              pOsInterface,
        PMOS_RESOURCE               pResource);
        
    void (* pfnFreeResourceWithFlag) (
        PMOS_INTERFACE              pOsInterface,
        PMOS_RESOURCE               pResource,
        uint32_t                    uiFlag); // for surface free
        
    void  *(* pfnLockResource) (
        PMOS_INTERFACE              pOsInterface,
        PMOS_RESOURCE               pResource,
        PMOS_LOCK_PARAMS            pFlags);
        
    MOS_STATUS (* pfnUnlockResource) (
        PMOS_INTERFACE              pOsInterface,
        PMOS_RESOURCE               pResource);
        
    MOS_STATUS(*pfnSkipResourceSync)(
        PMOS_RESOURCE               pOsResource);
        
    void (* pfnSyncOnResource) (
        PMOS_INTERFACE              pOsInterface,
        PMOS_RESOURCE               pOsResource,
        MOS_GPU_CONTEXT             requestorGPUCtx,
        int32_t                     bWriteOperation);
        
    MOS_STATUS (*pfnUpdateResourceUsageType) (
        PMOS_RESOURCE           pOsResource,
        MOS_HW_RESOURCE_DEF     resUsageType);
} MOS_INTERFACE *PMOS_INTERFACE;
```

## CtxMgr.cpp
This is GPU context and cmdbuffer execution management.
