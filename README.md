## Adaptor
This is top adaptor including some public interface for uplayer caller integration.

## PkgMgr.cpp
This is 2nd layer under Adaptor to pass call requirement from adaptor to internal calling.

## StatusMgr.cpp
This is parallel layer as PkgMgr for GPU execution status management.

## ItfMgr.cpp
This is hw interface management which may contains different sub-hw interface. For pkgMgr preparing hw cmd instruction.

## ResMgr.cpp
This is hw resource management.

## CtxMgr.cpp
This is GPU context and cmdbuffer execution management.
