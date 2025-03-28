# scripts/dtc makefile

hostprogs-y := dtc
always := $(hostprogs-y)

# dtc のオブジェクトファイル
dtc-objs := dtc.o flattree.o fstree.o data.o livetree.o treesource.o \
           srcpos.o checks.o util.o
dtc-objs += dtc-lexer.lex.o dtc-parser.tab.o

# Source files need to get at the userspace version of libfdt_env.h to compile
HOSTCFLAGS_DTC := -I$(src) -I$(src)/libfdt

HOSTCFLAGS_checks.o := $(HOSTCFLAGS_DTC)
HOSTCFLAGS_data.o := $(HOSTCFLAGS_DTC)
HOSTCFLAGS_dtc.o := $(HOSTCFLAGS_DTC)
HOSTCFLAGS_flattree.o := $(HOSTCFLAGS_DTC)
HOSTCFLAGS_fstree.o := $(HOSTCFLAGS_DTC)
HOSTCFLAGS_livetree.o := $(HOSTCFLAGS_DTC)
HOSTCFLAGS_srcpos.o := $(HOSTCFLAGS_DTC)
HOSTCFLAGS_treesource.o := $(HOSTCFLAGS_DTC)
HOSTCFLAGS_util.o := $(HOSTCFLAGS_DTC)

HOSTCFLAGS_dtc-lexer.lex.o := $(HOSTCFLAGS_DTC)
HOSTCFLAGS_dtc-parser.tab.o := $(HOSTCFLAGS_DTC)

# dtc-parser.tab.h を生成するために必要なルール（bisonを使用）
$(obj)/dtc-parser.tab.h: $(srctree)/scripts/dtc/dtc-parser.y
	bison -d $(srctree)/scripts/dtc/dtc-parser.y -o $(obj)/dtc-parser.tab.c

# dtc-lexer.lex.o と dtc-parser.tab.o の依存関係
$(obj)/dtc-lexer.lex.o: $(obj)/dtc-parser.tab.h $(obj)/dtc-parser.tab.c
	$(HOSTCC) $(HOSTCFLAGS_dtc-lexer.lex.o) -c -o $@ $<

$(obj)/dtc-parser.tab.o: $(obj)/dtc-parser.tab.h $(obj)/dtc-parser.tab.c
	$(HOSTCC) $(HOSTCFLAGS_dtc-parser.tab.o) -c -o $@ $<

# clean-files に追加するために生成するファイルを明示的に指定
clean-files := dtc-lexer.lex.c dtc-parser.tab.c dtc-parser.tab.h \
               dtc-lexer.lex.o dtc-parser.tab.o
