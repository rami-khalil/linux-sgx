#
# Copyright (C) 2011-2016 Intel Corporation. All rights reserved.
#
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions
# are met:
#
#   * Redistributions of source code must retain the above copyright
#     notice, this list of conditions and the following disclaimer.
#   * Redistributions in binary form must reproduce the above copyright
#     notice, this list of conditions and the following disclaimer in
#     the documentation and/or other materials provided with the
#     distribution.
#   * Neither the name of Intel Corporation nor the names of its
#     contributors may be used to endorse or promote products derived
#     from this software without specific prior written permission.
#
# THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
# "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
# LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
# A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT
# OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
# SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT
# LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE,
# DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY
# THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
# (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
# OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
#
#

parent-dir = $(patsubst %/,%,$(dir $(1:%/=%)))
my-dir     = $(call parent-dir,$(lastword $(MAKEFILE_LIST)))
################################################################################

LOCAL_PATH  := $(call my-dir)
BASE_DIR    := $(LOCAL_PATH)/../../../..
ANDROID_DIR := $(BASE_DIR)/android
include $(BASE_DIR)/buildenv.mk
PROTOC      := protoc
################################################################################

proto_sources              := messages.proto
proto_sources_fullpath     := $(addprefix $(LOCAL_PATH)/, $(proto_sources))
proto_generated_cc_sources := $(patsubst %.proto,%.pb.cc,$(proto_sources_fullpath))
proto_generated_headers    := $(patsubst %.pb.cc,%.pb.h, $(proto_generated_cc_sources))

.PHONY: all clean

all: $(proto_generated_headers)

$(proto_generated_headers):    %.pb.h:  %.pb.cc

$(proto_generated_cc_sources): PRIVATE_PROTO_OUT_DIR  := $(LOCAL_PATH)
$(proto_generated_cc_sources): PRIVATE_PROTO_PATH_DIR := $(LOCAL_PATH)
$(proto_generated_cc_sources): %.pb.cc: %.proto
	$(PROTOC) --cpp_out=$(PRIVATE_PROTO_OUT_DIR) --proto_path=$(PRIVATE_PROTO_PATH_DIR) $^

clean::
	rm -f $(proto_generated_cc_sources) $(proto_generated_headers)
