.PHONY: clean
GHDL=ghdl
GHDLFLAGS=--ieee=synopsys
SIMULATION_WAVEFORM=ghw
SOURCE_FOLDER=..

NON_LINEAR_OBJ=\
	$(SOURCE_FOLDER)/gimli_non_linear_permutation.o \
	$(SOURCE_FOLDER)/gimli_all_columns_non_linear_permutation.o

ALL_COMBINATIONAL_OBJ=\
	$(NON_LINEAR_OBJ)\
	$(SOURCE_FOLDER)/gimli_all_combinational.o
TB_ALL_COMBINATIONAL=tb_gimli_all_combinational

ALL_COMBINATIONAL_WITH_COMM_OBJ=\
	$(ALL_COMBINATIONAL_OBJ)\
	$(SOURCE_FOLDER)/gimli_all_combinational_with_communication.o
TB_ALL_COMBINATIONAL_WITH_COMM=tb_gimli_all_combinational_with_communication

HALF_COMBINATIONAL_WITH_COMM_OBJ=\
	$(NON_LINEAR_OBJ)\
	$(SOURCE_FOLDER)/gimli_half_combinational.o\
	$(SOURCE_FOLDER)/gimli_half_combinational_with_communication.o
TB_HALF_COMBINATIONAL_WITH_COMM=tb_gimli_half_combinational_with_communication

ROUNDS_COMBINATIONAL_WITH_COMM_OBJ=\
	$(NON_LINEAR_OBJ)\
	$(SOURCE_FOLDER)/gimli_rounds_combinational.o \
	$(SOURCE_FOLDER)/gimli_rounds_combinational_with_communication.o
TB_ROUNDS_COMBINATIONAL_WITH_COMM=tb_gimli_rounds_combinational_with_communication

SERIAL_COMBINATIONAL_WITH_COMM_OBJ=\
	$(NON_LINEAR_OBJ)\
	$(SOURCE_FOLDER)/gimli_serial_combinational_with_communication.o
TB_SERIAL_COMBINATIONAL_WITH_COMM=tb_gimli_serial_combinational_with_communication

ALL_TESTBENCHES=\
	$(TB_ALL_COMBINATIONAL).$(SIMULATION_WAVEFORM)\
	$(TB_HALF_COMBINATIONAL_WITH_COMM).$(SIMULATION_WAVEFORM)\
	$(TB_ALL_COMBINATIONAL_WITH_COMM).$(SIMULATION_WAVEFORM)\
	$(TB_ROUNDS_COMBINATIONAL_WITH_COMM).$(SIMULATION_WAVEFORM)\
	$(TB_SERIAL_COMBINATIONAL_WITH_COMM).$(SIMULATION_WAVEFORM)

test_all_combinational: $(ALL_COMBINATIONAL_OBJ)
	$(GHDL) -a $(GHDLFLAGS) $(SOURCE_FOLDER)/$(TB_ALL_COMBINATIONAL).vhd
	$(GHDL) -e $(GHDLFLAGS) $(TB_ALL_COMBINATIONAL)
	$(GHDL) -r $(GHDLFLAGS) $(TB_ALL_COMBINATIONAL) --wave=$(TB_ALL_COMBINATIONAL).$(SIMULATION_WAVEFORM)

test_half_combinational_with_comm: $(HALF_COMBINATIONAL_WITH_COMM_OBJ)
	$(GHDL) -a $(GHDLFLAGS) $(SOURCE_FOLDER)/$(TB_HALF_COMBINATIONAL_WITH_COMM).vhd
	$(GHDL) -e $(GHDLFLAGS) $(TB_HALF_COMBINATIONAL_WITH_COMM)
	$(GHDL) -r $(GHDLFLAGS) $(TB_HALF_COMBINATIONAL_WITH_COMM) --wave=$(TB_HALF_COMBINATIONAL_WITH_COMM).$(SIMULATION_WAVEFORM)

test_all_combinational_with_comm: $(ALL_COMBINATIONAL_WITH_COMM_OBJ)
	$(GHDL) -a $(GHDLFLAGS) $(SOURCE_FOLDER)/$(TB_ALL_COMBINATIONAL_WITH_COMM).vhd
	$(GHDL) -e $(GHDLFLAGS) $(TB_ALL_COMBINATIONAL_WITH_COMM)
	$(GHDL) -r $(GHDLFLAGS) $(TB_ALL_COMBINATIONAL_WITH_COMM) --wave=$(TB_ALL_COMBINATIONAL_WITH_COMM).$(SIMULATION_WAVEFORM)

test_rounds_combinational_with_comm: $(ROUNDS_COMBINATIONAL_WITH_COMM_OBJ)
	$(GHDL) -a $(GHDLFLAGS) $(SOURCE_FOLDER)/$(TB_ROUNDS_COMBINATIONAL_WITH_COMM).vhd
	$(GHDL) -e $(GHDLFLAGS) $(TB_ROUNDS_COMBINATIONAL_WITH_COMM)
	$(GHDL) -r $(GHDLFLAGS) $(TB_ROUNDS_COMBINATIONAL_WITH_COMM) --wave=$(TB_ROUNDS_COMBINATIONAL_WITH_COMM).$(SIMULATION_WAVEFORM)

test_serial_combinational_with_comm: $(SERIAL_COMBINATIONAL_WITH_COMM_OBJ)
	$(GHDL) -a $(GHDLFLAGS) $(SOURCE_FOLDER)/$(TB_SERIAL_COMBINATIONAL_WITH_COMM).vhd
	$(GHDL) -e $(GHDLFLAGS) $(TB_SERIAL_COMBINATIONAL_WITH_COMM)
	$(GHDL) -r $(GHDLFLAGS) $(TB_SERIAL_COMBINATIONAL_WITH_COMM) --wave=$(TB_SERIAL_COMBINATIONAL_WITH_COMM).$(SIMULATION_WAVEFORM)


# Binary depends on the object file
%: %.o
	$(GHDL) -e $(GHDLFLAGS) $@

# Object file depends on source
%.o: %.vhd
	$(GHDL) -a $(GHDLFLAGS) $<


clean:
	@echo "Cleaning up..."
	rm -f $(ALL_TESTBENCHES)
	rm -f work*.cf
	@echo "Cleaning done."
