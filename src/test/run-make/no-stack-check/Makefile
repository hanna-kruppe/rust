-include ../tools.mk

SKIP_OS := 'MINGW OpenBSD Bitrig'

ifneq ($(UNAME),$(findstring $(UNAME),$(SKIP_OS)))

all:
	$(RUSTC) -O --emit asm attr.rs
	! grep -q morestack $(TMPDIR)/attr.s
	$(RUSTC) -O --emit asm flag.rs
	grep -q morestack $(TMPDIR)/flag.s
	$(RUSTC) -O --emit asm -C no-stack-check flag.rs
	! grep -q morestack $(TMPDIR)/flag.s
else
# On Windows we use __chkstk and it only appears in functions with large allocations,
# so this test wouldn't be reliable.
# On Bitrig/OpenBSD, morestack isn't used as the segmented stacks are disabled
all:
endif
