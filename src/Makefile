OPTIMIZE=$(OPT)

ifneq ($(OPTIMIZE), true)
	OPTFLAGS=-O0 -g -Wall -Wextra -Wmissing-prototypes -Wold-style-definition # -Werror
	OBJDIR=build/debug
else
	OPTFLAGS=-O2 -g
	OBJDIR=build/optimized
endif

DEPSDIR=$(OBJDIR)/deps

CFLAGS=-DLIBGDK -DLIBMAL -DLIBOPTIMIZER -DLIBSTREAM

LDFLAGS=-lm -lpthread -ldl
CFLAGS += -Imonetdblite/src/ -Imonetdblite/src/common  \
-Imonetdblite/src/embedded -Imonetdblite/src/gdk \
-Imonetdblite/src/mal/mal -Imonetdblite/src/mal/modules -Imonetdblite/src/mal/optimizer -Imonetdblite/src/mal/sqlbackend \
-Imonetdblite/src/sql/include -Imonetdblite/src/sql/common -Imonetdblite/src/sql/server -Imonetdblite/src/sql/storage -Imonetdblite/src/sql/storage/bat

SOEXT=so
		
ifeq ($(OS),Windows_NT)
	SOEXT=dll
	CC=gcc
    CFLAGS += -DWIN32 -D__CYGWIN__
#    ifeq ($(PROCESSOR_ARCHITEW6432),AMD64)
#        CFLAGS += -D AMD64
#    else
#        ifeq ($(PROCESSOR_ARCHITECTURE),AMD64)
#            CFLAGS += -D AMD64
#        endif
#        ifeq ($(PROCESSOR_ARCHITECTURE),x86)
#            CFLAGS += -D IA32
#        endif
#    endif
else
    UNAME_S := $(shell uname -s)
    CFLAGS += -fPIC
    ifeq ($(UNAME_S),Linux)
		LDFLAGS += -lrt
    endif
    ifeq ($(UNAME_S),Darwin)
		#SOEXT=dylib
    endif
endif


OBJECTS=\
$(OBJDIR)/embeddedpy/conversion.o \
$(OBJDIR)/embeddedpy/embeddedpy.o \
$(OBJDIR)/embeddedpy/pytypes.o \
$(OBJDIR)/embeddedpy/type_conversion.o \
$(OBJDIR)/embeddedpy/unicode.o \
$(OBJDIR)/monetdblite/common/stream.o \
$(OBJDIR)/monetdblite/common/mutils.o \
$(OBJDIR)/monetdblite/embedded/embedded.o \
$(OBJDIR)/monetdblite/gdk/gdk_aggr.o \
$(OBJDIR)/monetdblite/gdk/gdk_align.o \
$(OBJDIR)/monetdblite/gdk/gdk_atoms.o \
$(OBJDIR)/monetdblite/gdk/gdk_bat.o \
$(OBJDIR)/monetdblite/gdk/gdk_batop.o \
$(OBJDIR)/monetdblite/gdk/gdk_bbp.o \
$(OBJDIR)/monetdblite/gdk/gdk_calc.o \
$(OBJDIR)/monetdblite/gdk/gdk_cross.o \
$(OBJDIR)/monetdblite/gdk/gdk_delta.o \
$(OBJDIR)/monetdblite/gdk/gdk_firstn.o \
$(OBJDIR)/monetdblite/gdk/gdk_group.o \
$(OBJDIR)/monetdblite/gdk/gdk_hash.o \
$(OBJDIR)/monetdblite/gdk/gdk_heap.o \
$(OBJDIR)/monetdblite/gdk/gdk_imprints.o \
$(OBJDIR)/monetdblite/gdk/gdk_join.o \
$(OBJDIR)/monetdblite/gdk/gdk_logger.o \
$(OBJDIR)/monetdblite/gdk/gdk_orderidx.o \
$(OBJDIR)/monetdblite/gdk/gdk_posix.o \
$(OBJDIR)/monetdblite/gdk/gdk_project.o \
$(OBJDIR)/monetdblite/gdk/gdk_qsort.o \
$(OBJDIR)/monetdblite/gdk/gdk_sample.o \
$(OBJDIR)/monetdblite/gdk/gdk_search.o \
$(OBJDIR)/monetdblite/gdk/gdk_select.o \
$(OBJDIR)/monetdblite/gdk/gdk_ssort.o \
$(OBJDIR)/monetdblite/gdk/gdk_storage.o \
$(OBJDIR)/monetdblite/gdk/gdk_system.o \
$(OBJDIR)/monetdblite/gdk/gdk_tm.o \
$(OBJDIR)/monetdblite/gdk/gdk_unique.o \
$(OBJDIR)/monetdblite/gdk/gdk_utils.o \
$(OBJDIR)/monetdblite/gdk/gdk_value.o \
$(OBJDIR)/monetdblite/mal/mal/mal.o \
$(OBJDIR)/monetdblite/mal/mal/mal_atom.o \
$(OBJDIR)/monetdblite/mal/mal/mal_builder.o \
$(OBJDIR)/monetdblite/mal/mal/mal_client.o \
$(OBJDIR)/monetdblite/mal/mal/mal_dataflow.o \
$(OBJDIR)/monetdblite/mal/mal/mal_exception.o \
$(OBJDIR)/monetdblite/mal/mal/mal_function.o \
$(OBJDIR)/monetdblite/mal/mal/mal_import.o \
$(OBJDIR)/monetdblite/mal/mal/mal_instruction.o \
$(OBJDIR)/monetdblite/mal/mal/mal_interpreter.o \
$(OBJDIR)/monetdblite/mal/mal/mal_linker.o \
$(OBJDIR)/monetdblite/mal/mal/mal_listing.o \
$(OBJDIR)/monetdblite/mal/mal/mal_module.o \
$(OBJDIR)/monetdblite/mal/mal/mal_namespace.o \
$(OBJDIR)/monetdblite/mal/mal/mal_parser.o \
$(OBJDIR)/monetdblite/mal/mal/mal_resolve.o \
$(OBJDIR)/monetdblite/mal/mal/mal_runtime.o \
$(OBJDIR)/monetdblite/mal/mal/mal_scenario.o \
$(OBJDIR)/monetdblite/mal/mal/mal_session.o \
$(OBJDIR)/monetdblite/mal/mal/mal_stack.o \
$(OBJDIR)/monetdblite/mal/mal/mal_type.o \
$(OBJDIR)/monetdblite/mal/mal/mal_utils.o \
$(OBJDIR)/monetdblite/mal/modules/aggr.o \
$(OBJDIR)/monetdblite/mal/modules/algebra.o \
$(OBJDIR)/monetdblite/mal/modules/bat5.o \
$(OBJDIR)/monetdblite/mal/modules/batcalc.o \
$(OBJDIR)/monetdblite/mal/modules/batExtensions.o \
$(OBJDIR)/monetdblite/mal/modules/batmmath.o \
$(OBJDIR)/monetdblite/mal/modules/batstr.o \
$(OBJDIR)/monetdblite/mal/modules/blob.o \
$(OBJDIR)/monetdblite/mal/modules/calc.o \
$(OBJDIR)/monetdblite/mal/modules/group.o \
$(OBJDIR)/monetdblite/mal/modules/iterator.o \
$(OBJDIR)/monetdblite/mal/modules/language.o \
$(OBJDIR)/monetdblite/mal/modules/manifold.o \
$(OBJDIR)/monetdblite/mal/modules/mat.o \
$(OBJDIR)/monetdblite/mal/modules/mkey.o \
$(OBJDIR)/monetdblite/mal/modules/mmath.o \
$(OBJDIR)/monetdblite/mal/modules/mtime.o \
$(OBJDIR)/monetdblite/mal/modules/orderidx.o \
$(OBJDIR)/monetdblite/mal/modules/pcre.o \
$(OBJDIR)/monetdblite/mal/modules/projectionpath.o \
$(OBJDIR)/monetdblite/mal/modules/sample.o \
$(OBJDIR)/monetdblite/mal/modules/str.o \
$(OBJDIR)/monetdblite/mal/modules/tablet.o \
$(OBJDIR)/monetdblite/mal/optimizer/opt_aliases.o \
$(OBJDIR)/monetdblite/mal/optimizer/opt_candidates.o \
$(OBJDIR)/monetdblite/mal/optimizer/opt_coercion.o \
$(OBJDIR)/monetdblite/mal/optimizer/opt_commonTerms.o \
$(OBJDIR)/monetdblite/mal/optimizer/opt_constants.o \
$(OBJDIR)/monetdblite/mal/optimizer/opt_costModel.o \
$(OBJDIR)/monetdblite/mal/optimizer/opt_dataflow.o \
$(OBJDIR)/monetdblite/mal/optimizer/opt_deadcode.o \
$(OBJDIR)/monetdblite/mal/optimizer/opt_emptybind.o \
$(OBJDIR)/monetdblite/mal/optimizer/opt_evaluate.o \
$(OBJDIR)/monetdblite/mal/optimizer/opt_garbageCollector.o \
$(OBJDIR)/monetdblite/mal/optimizer/opt_generator.o \
$(OBJDIR)/monetdblite/mal/optimizer/opt_inline.o \
$(OBJDIR)/monetdblite/mal/optimizer/opt_macro.o \
$(OBJDIR)/monetdblite/mal/optimizer/opt_matpack.o \
$(OBJDIR)/monetdblite/mal/optimizer/opt_mergetable.o \
$(OBJDIR)/monetdblite/mal/optimizer/opt_mitosis.o \
$(OBJDIR)/monetdblite/mal/optimizer/opt_multiplex.o \
$(OBJDIR)/monetdblite/mal/optimizer/opt_pipes.o \
$(OBJDIR)/monetdblite/mal/optimizer/opt_prelude.o \
$(OBJDIR)/monetdblite/mal/optimizer/opt_profiler.o \
$(OBJDIR)/monetdblite/mal/optimizer/opt_projectionpath.o \
$(OBJDIR)/monetdblite/mal/optimizer/opt_pushselect.o \
$(OBJDIR)/monetdblite/mal/optimizer/opt_remap.o \
$(OBJDIR)/monetdblite/mal/optimizer/opt_reorder.o \
$(OBJDIR)/monetdblite/mal/optimizer/opt_support.o \
$(OBJDIR)/monetdblite/mal/optimizer/opt_wrapper.o \
$(OBJDIR)/monetdblite/mal/optimizer/optimizer.o \
$(OBJDIR)/monetdblite/mal/sqlbackend/mal_backend.o \
$(OBJDIR)/monetdblite/mal/sqlbackend/rel_bin.o \
$(OBJDIR)/monetdblite/mal/sqlbackend/sql.o \
$(OBJDIR)/monetdblite/mal/sqlbackend/sql_assert.o \
$(OBJDIR)/monetdblite/mal/sqlbackend/sql_bat2time.o \
$(OBJDIR)/monetdblite/mal/sqlbackend/sql_cast.o \
$(OBJDIR)/monetdblite/mal/sqlbackend/sql_cat.o \
$(OBJDIR)/monetdblite/mal/sqlbackend/sql_execute.o \
$(OBJDIR)/monetdblite/mal/sqlbackend/sql_fround.o \
$(OBJDIR)/monetdblite/mal/sqlbackend/sql_gencode.o \
$(OBJDIR)/monetdblite/mal/sqlbackend/sql_optimizer.o \
$(OBJDIR)/monetdblite/mal/sqlbackend/sql_orderidx.o \
$(OBJDIR)/monetdblite/mal/sqlbackend/sql_rank.o \
$(OBJDIR)/monetdblite/mal/sqlbackend/sql_result.o \
$(OBJDIR)/monetdblite/mal/sqlbackend/sql_round.o \
$(OBJDIR)/monetdblite/mal/sqlbackend/sql_scenario.o \
$(OBJDIR)/monetdblite/mal/sqlbackend/sql_statement.o \
$(OBJDIR)/monetdblite/mal/sqlbackend/sql_statistics.o \
$(OBJDIR)/monetdblite/mal/sqlbackend/sql_transaction.o \
$(OBJDIR)/monetdblite/mal/sqlbackend/sql_upgrades.o \
$(OBJDIR)/monetdblite/mal/sqlbackend/sql_user.o \
$(OBJDIR)/monetdblite/sql/common/sql_backend.o \
$(OBJDIR)/monetdblite/sql/common/sql_changeset.o \
$(OBJDIR)/monetdblite/sql/common/sql_hash.o \
$(OBJDIR)/monetdblite/sql/common/sql_keyword.o \
$(OBJDIR)/monetdblite/sql/common/sql_list.o \
$(OBJDIR)/monetdblite/sql/common/sql_mem.o \
$(OBJDIR)/monetdblite/sql/common/sql_stack.o \
$(OBJDIR)/monetdblite/sql/common/sql_string.o \
$(OBJDIR)/monetdblite/sql/common/sql_types.o \
$(OBJDIR)/monetdblite/sql/server/rel_distribute.o \
$(OBJDIR)/monetdblite/sql/server/rel_dump.o \
$(OBJDIR)/monetdblite/sql/server/rel_exp.o \
$(OBJDIR)/monetdblite/sql/server/rel_optimizer.o \
$(OBJDIR)/monetdblite/sql/server/rel_partition.o \
$(OBJDIR)/monetdblite/sql/server/rel_planner.o \
$(OBJDIR)/monetdblite/sql/server/rel_prop.o \
$(OBJDIR)/monetdblite/sql/server/rel_psm.o \
$(OBJDIR)/monetdblite/sql/server/rel_rel.o \
$(OBJDIR)/monetdblite/sql/server/rel_remote.o \
$(OBJDIR)/monetdblite/sql/server/rel_schema.o \
$(OBJDIR)/monetdblite/sql/server/rel_select.o \
$(OBJDIR)/monetdblite/sql/server/rel_semantic.o \
$(OBJDIR)/monetdblite/sql/server/rel_sequence.o \
$(OBJDIR)/monetdblite/sql/server/rel_trans.o \
$(OBJDIR)/monetdblite/sql/server/rel_updates.o \
$(OBJDIR)/monetdblite/sql/server/rel_xml.o \
$(OBJDIR)/monetdblite/sql/server/sql_atom.o \
$(OBJDIR)/monetdblite/sql/server/sql_datetime.o \
$(OBJDIR)/monetdblite/sql/server/sql_decimal.o \
$(OBJDIR)/monetdblite/sql/server/sql_env.o \
$(OBJDIR)/monetdblite/sql/server/sql_mvc.o \
$(OBJDIR)/monetdblite/sql/server/sql_parser.tab.o \
$(OBJDIR)/monetdblite/sql/server/sql_privileges.o \
$(OBJDIR)/monetdblite/sql/server/sql_qc.o \
$(OBJDIR)/monetdblite/sql/server/sql_scan.o \
$(OBJDIR)/monetdblite/sql/server/sql_semantic.o \
$(OBJDIR)/monetdblite/sql/server/sql_symbol.o \
$(OBJDIR)/monetdblite/sql/storage/bat/bat_logger.o \
$(OBJDIR)/monetdblite/sql/storage/bat/bat_storage.o \
$(OBJDIR)/monetdblite/sql/storage/bat/bat_table.o \
$(OBJDIR)/monetdblite/sql/storage/bat/bat_utils.o \
$(OBJDIR)/monetdblite/sql/storage/bat/nop_logger.o \
$(OBJDIR)/monetdblite/sql/storage/bat/res_table.o \
$(OBJDIR)/monetdblite/sql/storage/sql_catalog.o \
$(OBJDIR)/monetdblite/sql/storage/store.o \
$(OBJDIR)/monetdblite/sql/storage/store_dependency.o \
$(OBJDIR)/monetdblite/sql/storage/store_sequence.o


ODIRS=$(dir $(OBJECTS))
DDIRS=$(subst $(OBJDIR), $(DEPSDIR), $(ODIRS))
$(shell mkdir -p $(ODIRS) $(DDIRS))


LIBFILE=build/libmonetdb5.$(SOEXT)

.PHONY: all clean $(LIBFILE)

all: $(OBJECTS) $(LIBFILE)

clean:
	rm -rf build


$(OBJDIR)/monetdblite/%.o: monetdblite/src/%.c
	$(CC) $(CFLAGS) -MMD -MF $(subst $(OBJDIR),$(DEPSDIR),$(subst .o,.d,$@)) $(OPTFLAGS) -c $(subst $(OBJDIR)/monetdblite,monetdblite/src,$(subst .o,.c,$@)) -o $@

$(OBJDIR)/embeddedpy/%.o: embeddedpy/%.c
	$(CC) $(CFLAGS) $(MONETDBLITE_PYTHON_INCLUDE_FLAGS) -MMD -MF $(subst $(OBJDIR),$(DEPSDIR),$(subst .o,.d,$@)) $(OPTFLAGS) -c $(subst $(OBJDIR)/,,$(subst .o,.c,$@)) -o $@

$(LIBFILE): $(OBJECTS) 
	$(CC) $(LDFLAGS) $(MONETDBLITE_PYTHON_LINK_FLAGS) $(OBJECTS) $(OPTFLAGS) -o $(LIBFILE) -shared
