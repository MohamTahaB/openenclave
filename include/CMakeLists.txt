# Copyright (c) Open Enclave SDK contributors.
# Licensed under the MIT License.

# OE main include files, add interface library, add install steps

add_library(oe_includes INTERFACE)
target_include_directories(
  oe_includes
  INTERFACE $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
            $<BUILD_INTERFACE:${OE_INCDIR}>
            $<INSTALL_INTERFACE:$<INSTALL_PREFIX>/${CMAKE_INSTALL_INCLUDEDIR}>)
install(
  DIRECTORY openenclave/bits
  DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/openenclave/
  COMPONENT OEHOSTVERIFY)
install(FILES openenclave/debugmalloc.h
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/openenclave/)
install(DIRECTORY openenclave/edger8r
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/openenclave/)
install(FILES openenclave/enclave.h
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/openenclave/)
install(FILES openenclave/host.h
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/openenclave/)
install(FILES openenclave/log.h
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/openenclave/)
install(FILES openenclave/trace.h
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/openenclave/)
install(FILES openenclave/tracee.h
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/openenclave/)
install(
  FILES openenclave/host_verify.h
  DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/openenclave/
  COMPONENT OEHOSTVERIFY)
install(FILES openenclave/attestation/attester.h
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/openenclave/attestation/)
install(
  FILES openenclave/attestation/sgx/eeid_attester.h
        openenclave/attestation/sgx/eeid_plugin.h
        openenclave/attestation/sgx/eeid_verifier.h
  DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/openenclave/attestation/sgx)
install(
  FILES openenclave/attestation/verifier.h
        openenclave/attestation/custom_claims.h
  DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/openenclave/attestation/
  COMPONENT OEHOSTVERIFY)
install(
  FILES openenclave/attestation/sgx/report.h
        openenclave/attestation/sgx/evidence.h
  DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/openenclave/attestation/sgx/
  COMPONENT OEHOSTVERIFY)
install(TARGETS oe_includes EXPORT openenclave-targets)
install(
  TARGETS oe_includes
  EXPORT openenclave-hostverify-targets
  COMPONENT OEHOSTVERIFY)
install(FILES openenclave/seal.h
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/openenclave)
install(DIRECTORY openenclave/sgx
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/openenclave)

# Install parts of oelibc needed by edger8r-generated code
list(
  APPEND
  CORELIBC_DEPS
  openenclave/corelibc/errno.h
  openenclave/corelibc/limits.h
  openenclave/corelibc/stdlib.h
  openenclave/corelibc/string.h
  openenclave/corelibc/wchar.h)
install(FILES ${CORELIBC_DEPS}
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/openenclave/corelibc)
install(FILES openenclave/corelibc/bits/defs.h
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/openenclave/corelibc/bits)
install(FILES openenclave/corelibc/bits/types.h
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/openenclave/corelibc/bits)

# Install pluggable allocator header.
install(FILES openenclave/advanced/allocator.h
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/openenclave/advanced)

# Install allocator info header.
install(FILES openenclave/advanced/mallinfo.h
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/openenclave/advanced)

##==============================================================================
##
## Install all system EDL files to be included by user EDL
##
##==============================================================================

install(DIRECTORY ./openenclave/edl/
        DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/openenclave/edl/)
