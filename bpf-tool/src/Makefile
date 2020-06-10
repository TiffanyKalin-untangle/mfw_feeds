#
# Copyright (C) 2014 Jakub Kicinski <kubakici@wp.pl>
# Copyright (C) 2017 Netoronome Systems, Inc.
#
# This software is dual licensed under the GNU General License Version 2,
# June 1991 as shown in the file COPYING in the top-level directory of this
# source tree or the BSD 2-Clause License provided below.  You have the
# option to license this software under the complete terms of either license.
#
# The BSD 2-Clause License:
#
#     Redistribution and use in source and binary forms, with or
#     without modification, are permitted provided that the following
#     conditions are met:
#
#      1. Redistributions of source code must retain the above
#         copyright notice, this list of conditions and the following
#         disclaimer.
#
#      2. Redistributions in binary form must reproduce the above
#         copyright notice, this list of conditions and the following
#         disclaimer in the documentation and/or other materials
#         provided with the distribution.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
# EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
# MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
# NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS
# BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN
# ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
# CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.
#

BPFTOOL_VERSION = 4.18.0

CFLAGS += -O2 -W -Wall -Wextra -Wno-unused-parameter -Wno-missing-field-initializers
CFLAGS += -I/home/untangles/openwrt/build_dir/toolchain-x86_64_gcc-7.3.0_musl/linux-4.14.131/kernel/bpf
CFLAGS += -I/home/untangles/openwrt/build_dir/toolchain-x86_64_gcc-7.3.0_musl/linux-4.14.131/tools/include
CFLAGS += -I/home/untangles/openwrt/build_dir/toolchain-x86_64_gcc-7.3.0_musl/linux-4.14.131/tools/include/uapi
CFLAGS += -I/home/untangles/openwrt/build_dir/toolchain-x86_64_gcc-7.3.0_musl/linux-4.14.131/tools/lib/bpf
CFLAGS += -I/home/untangles/openwrt/build_dir/toolchain-x86_64_gcc-7.3.0_musl/linux-4.14.131/tools/perf
#CFLAGS += -I/home/untangles/openwrt/build_dir/toolchain-x86_64_gcc-7.3.0_musl/linux-4.14.131/include/uapi
#CFLAGS += -I/home/untangles/openwrt/build_dir/toolchain-x86_64_gcc-7.3.0_musl/linux-4.14.131/include
CFLAGS += -DBPFTOOL_VERSION='"$(BPFTOOL_VERISON)"'
LDFLAGS += -lfts -lpthread -lbpf -lelf -lbfd -lopcodes

include $(wildcard *.d)

all: bpftool

bpftool: cfg.o cgroup.o common.o disasm.o jit_disasm.o json_writer.o main.o map.o prog.o xlated_dumper.o
	$(CC) $(CFLAGS) -o $@ $^ $(LDFLAGS)

clean:
	rm -rf *.o *.d *~

%.o: %.c
	$(COMPILE.c) -MMD -o $@ $<

.PHONY = all clean
.DEFAULT_GOAL = all
