# EXPERIMENT NO. 7

# SIMULATION AND IMPLEMENTATION OF FLIP-FLOPS, SHIFT REGISTERS, UP/DOWN COUNTER

### Submitted By

**R.K. Vageesh Ragav**
B.E. Electronics and Communication Engineering (ECE)
Saveetha Engineering College, Chennai

### Course

**EC1801 – Digital Logic Circuits Design Laboratory**

---

## AIM

To write VHDL programs for Flip-Flops, Shift Registers and Up/Down Counter and verify their operation through simulation. 

---

## SOFTWARE REQUIRED

1. Xilinx Vivado / Xilinx ISE
2. ModelSim
3. GHDL Simulator

---

# THEORY

### JK Flip-Flop

A JK Flip-Flop is a sequential circuit with two inputs (J and K) and a clock input. It eliminates the invalid state of the RS Flip-Flop.

### D Flip-Flop

A D Flip-Flop stores one bit of data and transfers the input to the output on the triggering edge of the clock.

### Shift Register

A Shift Register is a sequential circuit used to store and transfer data. Data can be shifted serially or loaded in parallel.

### Up/Down Counter

An Up/Down Counter counts upward or downward depending on the control signal.

---

# PROGRAMS

## JK FLIP-FLOP

```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity JK_FF is
    Port(
        J,K,CLK,RST : in STD_LOGIC;
        Q : out STD_LOGIC
    );
end JK_FF;

architecture Behavioral of JK_FF is
signal temp : STD_LOGIC := '0';
begin
process(CLK,RST)
begin
    if RST='1' then
        temp <= '0';
    elsif rising_edge(CLK) then
        case (J & K) is
            when "00" => temp <= temp;
            when "01" => temp <= '0';
            when "10" => temp <= '1';
            when "11" => temp <= not temp;
            when others => null;
        end case;
    end if;
end process;
Q <= temp;
end Behavioral;
```

---

## D FLIP-FLOP

```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity D_FF is
    Port(
        D,CLK,RST : in STD_LOGIC;
        Q : out STD_LOGIC
    );
end D_FF;

architecture Behavioral of D_FF is
signal temp : STD_LOGIC := '0';
begin
process(CLK,RST)
begin
    if RST='1' then
        temp <= '0';
    elsif rising_edge(CLK) then
        temp <= D;
    end if;
end process;
Q <= temp;
end Behavioral;
```

---

## SERIAL IN SERIAL OUT SHIFT REGISTER

```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity SISO is
    Port(
        CLK,RST,SI : in STD_LOGIC;
        SO : out STD_LOGIC
    );
end SISO;

architecture Behavioral of SISO is
signal shift_reg : STD_LOGIC_VECTOR(3 downto 0);
begin

process(CLK)
begin
    if rising_edge(CLK) then
        if RST='1' then
            shift_reg <= "0000";
        else
            shift_reg <= shift_reg(2 downto 0) & SI;
        end if;
    end if;
end process;

SO <= shift_reg(3);

end Behavioral;
```

---

## PARALLEL IN SERIAL OUT SHIFT REGISTER

```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;

entity PISO is
    Port(
        CLK,RST,LOAD : in STD_LOGIC;
        PARALLEL_IN : in STD_LOGIC_VECTOR(3 downto 0);
        SERIAL_OUT : out STD_LOGIC
    );
end PISO;

architecture Behavioral of PISO is
signal shift_reg : STD_LOGIC_VECTOR(3 downto 0);
begin

process(CLK)
begin
    if rising_edge(CLK) then
        if RST='1' then
            shift_reg <= "0000";
        elsif LOAD='1' then
            shift_reg <= PARALLEL_IN;
        else
            shift_reg <= shift_reg(2 downto 0) & '0';
        end if;
    end if;
end process;

SERIAL_OUT <= shift_reg(3);

end Behavioral;
```

---

## 4-BIT UP/DOWN COUNTER

```vhdl
library IEEE;
use IEEE.STD_LOGIC_1164.ALL;
use IEEE.NUMERIC_STD.ALL;

entity UP_DOWN_COUNTER is
    Port(
        CLK,RST,UP_DOWN : in STD_LOGIC;
        COUNT : out STD_LOGIC_VECTOR(3 downto 0)
    );
end UP_DOWN_COUNTER;

architecture Behavioral of UP_DOWN_COUNTER is
signal cnt : unsigned(3 downto 0) := "0000";
begin

process(CLK)
begin
    if rising_edge(CLK) then
        if RST='1' then
            cnt <= "0000";
        elsif UP_DOWN='1' then
            cnt <= cnt + 1;
        else
            cnt <= cnt - 1;
        end if;
    end if;
end process;

COUNT <= STD_LOGIC_VECTOR(cnt);

end Behavioral;
```

---

# OUTPUT

The simulation waveforms verify the operation of:

* JK Flip-Flop
* D Flip-Flop
* Serial In Serial Out Shift Register
* Parallel In Serial Out Shift Register
* 4-Bit Up/Down Counter

*(Insert waveform screenshots here)*

---

# RESULT

Thus, the Flip-Flops, Shift Registers and Up/Down Counter were successfully implemented using VHDL and verified through simulation waveforms. This corresponds to Experiment No. 7 in the laboratory manual. 

---

# AUTHOR DETAILS

**Name:** R.K. Vageesh Ragav
**Department:** Electronics and Communication Engineering (ECE)
**College:** Saveetha Engineering College
**Course Code:** EC1801 – Digital Logic Circuits Design Laboratory
**Experiment No.:** 7


