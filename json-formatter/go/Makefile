include default.mk

GOLDEN_JSONS = $(sort $(wildcard ../ruby/features/*.json))
GENERATED_JSONS = $(patsubst ../ruby/features/%.json,acceptance/%.json,$(GOLDEN_JSONS))

.DELETE_ON_ERROR:

.tested: $(GENERATED_JSONS)

acceptance/%.json: ../javascript/acceptance/%.ndjson $(EXE) ../ruby/features/%.json
	mkdir -p $$(dirname $@)
	cat $< | \
		$(EXE) --format ndjson | \
		../ruby/neutralize-json | \
		jq --sort-keys "." > \
		$@
	diff --unified $(word 3, $^) $@
