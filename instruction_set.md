BEAM Instruction Set
====================

Source: http://erlangonxen.org/more/beam


allocate
------------------------------
    allocate t t

Allocates Arg0 slots on the stack. Arg1 is Live.


allocate_heap
------------------------------
    allocate_heap t I t

Allocates Arg0 slots on the stack. See `allocate t t`. Ensures that heap
contains at least Arg1 words after __HTOP__. Arg2 is Live.


allocate_heap_zero
------------------------------
    allocate_heap_zero t I t

Same as `allocate_heap t I t` but sets the slots to nil.


allocate_init
------------------------------
    allocate_init t I y

Combines `allocate t I` and `init y`.


allocate_zero
------------------------------
    allocate_zero t t

Same as `allocate t t` but sets the slots to nil.


apply
------------------------------
    apply I

Finds the address from the export entry for the function (possibly BIF)
identified by the module R(N), the function R(N+1), and the arity N. The arity
is taken from Arg0. Sets __CP__ to the next instruction and jumps to the found
address.


apply_last
------------------------------
    apply_last I P

Similar to `apply I` but restores __CP__ from stack and drops Arg1 slots from
it before jumping to the found address.


badarg
------------------------------
    badarg j

If Arg0 is not 0 then jumps to the label Arg0. Otherwise, raises the badarg
exception.


badmatch
------------------------------
    badmatch rxy

Raises a badmatch exception with the value of Arg0.


bif1
------------------------------
    bif1 f b s d

Calls the BIF from Arg1 with the argument Arg2 and places the result to Arg3.
Upon error jumps to Arg0 as appropriate for the guard BIF.


bif1_body
------------------------------
    bif1_body b s d

Calls the BIF from Arg0 with the argument Argr1 and places the result to Arg3.
This is the case of a guard BIF in the function body. It fails like an ordinary
BIF.


bs_context_to_binary
------------------------------
    bs_context_to_binary rxy

Converts the matching context to a (sub)binary using almost the same code as
`i_bs_get_binary_all_reuse rx f I`.


bs_put_string
------------------------------
    bs_put_string I I

Assumes that previous instructions created a binary creation context. Packs a
string of characters Arg0 bytes long referenced by the pointer Arg1 into the
context.


bs_test_tail_imm2
------------------------------
    bs_test_tail_imm2 f rx I

Checks that the matching context Arg1 has exactly Arg2 unmatched bits. Jumps to
the label Arg0 if it is not so.


bs_test_unit
------------------------------
    bs_test_unit f rx I

Checks that the size of the remainder of the matching context Arg1 is divisible
by unit Arg2. Jumps to the label Arg0 if it is not so.


bs_test_unit8
------------------------------
    bs_test_unit8 f rx

Checks that the size of the remainder of the matching context Arg1 is divisible
by 8. Jumps to the label Arg1 if it is not.


bs_test_zero_tail2
------------------------------
    bs_test_zero_tail2 f rx

Jumps to the label in Arg0 if the matching context Arg1 still have unmatched
bits.


call_bif0
------------------------------
    call_bif0 e

Calls the BIF from Arg0 without arguments and returns result in R0.


call_bif1
------------------------------
    call_bif1 e

Calls the BIF from Arg0 with R0 as the argument and returns result in R0.


call_bif2
------------------------------
    call_bif2 e

Calls the BIF from Arg0 with arguments in R0 and R1 and returns result in R0.


call_bif3
------------------------------
    call_bif3 e

Calls the BIF from Arg0 with arguments in R0, R1, and R2 and returns result in
R0.


case_end
------------------------------
    case_end rxy

Raises a case_clause exception with the value of Arg0.


catch
------------------------------
    catch y f

Creates a new 'catch' context. Saves value of the label from Arg1 to the Arg0
stack slot.


catch_end
------------------------------
    catch_end y

Pops a 'catch' context. Erases the label saved in the Arg0 slot. Noval in R0
indicates that something is caught. If R1 contains atom 'throw' then R0 is set
to R2. If R1 contains atom 'error' R0 is set to `{'EXIT',{R2,<stacktrace>}}`.


deallocate
------------------------------
    deallocate I

Restores __CP__ to the value referenced by __EP__. Adds Arg0 + 1 to __EP__ to
remove the saved __CP__ and Arg0 slots from the stack.


deallocate_return
------------------------------
    deallocate_return Q

Combines `deallocate Q` and `return`.


extract_next_element
------------------------------
    extract_next_element xy

The pointer in __tmpA__ moved to the next element of the tuple. The element is
read from the location pointed to by __tmpA__ to Arg0.


extract_next_element2
------------------------------
    extract_next_element2 xy

The pointer in __tmpA__ moved to the next element of the tuple. Copies 2 terms
from the array pointed to by __tmpA__ to the registers or slots pointed to by
Arg0. For instance, if Arg0 is R3 then tuple elements are loaded to R3 and R4.


extract_next_element3
------------------------------
    extract_next_element3 xy

Same as `extract_next_element2 xy` but copies three elements.


fclearerror
------------------------------
    fclearerror

Maybe clears FP error flag.


fconv
------------------------------
    fconv d l

Converts Arg0 to float and places the result to Arg1.


fmove
------------------------------
    fmove qdl ld

Copies Arg0 to Arg1.


get_list
------------------------------
    get_list rxy rxy rxy

Gets the head of the list from Arg0 and puts it to Arg1, the tail - to Arg2.


i_apply
------------------------------
    i_apply

Applies the function identified by R0 (module), R1 (function), and R2
(arguments). Sets __CP__ to the point after the instruction.


i_apply_fun
------------------------------
    i_apply_fun

Applies the fun R0 to the argument list in R1. Set __CP__ to the location right
after the instruction.


i_apply_fun_last
------------------------------
    i_apply_fun_last P

Applies the fun R0 to the argument list in R1. Restores __CP__ from stack and
deallocates Arg0 slots from stack.


i_apply_fun_only
------------------------------
    i_apply_fun_only

Applies the fun R0 to the argument list in R1.


i_apply_last
------------------------------
    i_apply_last P

Applies the function identified by R0 (module), R1 (function), and R2
(arguments). Afterwards, restores __CP__ from stack and deallocates Arg0 slots
from stack.


i_apply_only
------------------------------
    i_apply_only

Applies the function identified by R0 (module), R1 (function), and R2
(arguments).


i_band
------------------------------
    i_band j I d

Arg2 = __tmpA__ & __tmpB__. Arg1 is Live. Jumps to Arg0 on error if Arg0 is not
zero.


i_bif2
------------------------------
    i_bif2 f b d

Calls the guard BIF from Arg1 with the two arguments in __tmpA__ and __tmpB__
and places the result to Arg2. Upon error jumps to Arg0 as appropriate for a
guard BIF.


i_bif2_body
------------------------------
    i_bif2_body b d

Calls the guard BIF from Arg0 with the two arguments in __tmpA__ and __tmpB__
and places the result to Arg1. This is the case of a guard BIF in the function
body.  It fails like an ordinary BIF.


i_bor
------------------------------
    i_bor j I d

Arg2 = __tmpA__ | __tmpB__. Arg1 is Live. Jumps to Arg0 on error if Arg0 is not
zero.


i_bs_add
------------------------------
    i_bs_add j I d

Calculates the total of the number of bits in __tmpA__ and the number of units
in __tmpB__. Arg1 is the unit. Stores the result to Arg2.


i_bs_append
------------------------------
    i_bs_append j I I I d

Appends __tmpA__ bits to a binary __tmpB__. If the binary is a writable
subbinary referencing a ProcBin with enough empty space then a new writable
subbinary is created and the old one is made non-writable. In other cases,
creates a new shared data, a new ProcBin, and a new subbinary. For all heap
allocation, a space for more Arg1 words are requested. Arg2 is Live. Arg3 is
unit. Saves the resultant subbinary to Arg4.


i_bs_get_binary2
------------------------------
    i_bs_get_binary2 f rx I s I d

Gets a binary from the matching context Arg1 of size (in units) Arg3. Arg2 is
Live. Arg4 are flags and unit. Puts result to Arg5. Jumps to Arg0 on failure.


i_bs_get_binary_all2
------------------------------
    i_bs_get_binary_all2 f rx I I d

Gets the rest of the matching context Arg1 as a binary and puts it to Arg4. The
binary size should be divisable by unit Arg3. Arg2 is Live. Jumps to Arg0 upon
failure.


i_bs_get_binary_all_reuse
------------------------------
    i_bs_get_binary_all_reuse rx f I

Replaces the matching context Arg0 with the rest of its reminder represented as
a binary. Arg2 is the unit. The size of the binary should be divisible by unit.
Jumps to the label Arg1 on failure.


i_bs_get_binary_imm2
------------------------------
    i_bs_get_binary_imm2 f rx I I I d

Gets a binary from the matching context Arg1 of size (in bits) Arg3. Arg2 is
Live. Arg4 are flags. The binary is put to Arg5. Jumps yo Arg0 on failure.


i_bs_get_float2
------------------------------
    i_bs_get_float2 f rx I s I d

Gets the float value form the matching context Arg1. Arg3 is the size in units.
Arg4 are unit and flags. Puts the value to Arg5. Arg2 is Live. Jumps to Arg0 on
failure.


i_bs_get_integer
------------------------------
    i_bs_get_integer f I I d

Gets an integer of size __tmpB__ (in units) from the matching context __tmpA__
and saves it to Arg3. Arg1 is Live.  Arg2 are flags and unit. Jumps to Arg0 on
failure.


i_bs_get_integer_16
------------------------------
    i_bs_get_integer_16 rx f d

Gets an 16-bit integer from the matching context Arg0 and saves it to Arg2.
Jumps to Arg1 if there are not enough bits left.


i_bs_get_integer_32
------------------------------
    i_bs_get_integer_32 rx f I d

Gets an 32-bit integer from the matching context Arg0 and saves it to Arg3.
Jumps to Arg1 if there are not enough bits left. Arg2 is Live as the integer
may not be small.


i_bs_get_integer_8
------------------------------
    i_bs_get_integer_8 rx f d

Gets an 8-bit integer from the matching context Arg0 and saves it to Arg2.
Jumps to Arg1 if there are not enough bits left.


i_bs_get_integer_imm
------------------------------
    i_bs_get_integer_imm rx I I f I d

Gets an integer of size (in bits) Arg1 from the matching context Arg0 and puts
it to Arg5. Arg4 are flags. Arg2 is Live. Jumps to the label Arg3 on failure.


i_bs_get_integer_small_imm
------------------------------
    i_bs_get_integer_small_imm rx I f I d

Gets a (small) integer of size (in bits) Arg1 from the matching context Arg0
and puts it to Arg4. Arg3 are flags. Jumps to the label Arg2 on failure.


i_bs_get_utf16
------------------------------
    i_bs_get_utf16 rx f I d

Extracts a UTF-16 encoded character from the matching context Arg0 using flags
Arg2 and places it to Arg3. Jumps to Arg1 upon failure.


i_bs_get_utf8
------------------------------
    i_bs_get_utf8 rx f d

Extracts a UTF-8 encoded character from the matching context Arg0 and places it
to Arg2. Jumps to Arg1 upon failure.


i_bs_init
------------------------------
    i_bs_init I I d

Allocates space for a shared binary data of Arg0 size. Creates a ProcBin
referencing the data. Makes sure that the heap has enough space for a subbinary.
Arg1 is Live. Puts the ProcBin into Arg2.


i_bs_init_bits
------------------------------
    i_bs_init_bits I I d

Same as `i_bs_init_bits_heap I I I d` but the number of extra words allocated
on heap is zero.


i_bs_init_bits_fail
------------------------------
    i_bs_init_bits_fail rxy j I d

Same as `i_bs_init_bits_heap I I I d` but the number of extra words allocated
on the heap is zero and may fail if the number of bits in Arg0 is not valid.
Arg1 is not used.


i_bs_init_bits_fail_heap
------------------------------
    i_bs_init_bits_fail_heap I j I d

Same as `i_bs_init_bits_heap I I I d` but the number of bits is fetched to
__tmpA__ by previous instruction and may fail if the number of bits in __tmpA__
is not valid. Arg1 is not used.


i_bs_init_bits_heap
------------------------------
    i_bs_init_bits_heap I I I d

Allocates a heap binary of size (in bits) Arg0. If the size is not divisible by
8 than allocates a subbinary referencing the exact number of bits of the heap
binary. Makes sure that heap has Arg1 extra words available. Arg2 is Live. Puts
the result (the heap binary or the subbinary) to Arg3.


i_bs_init_fail
------------------------------
    i_bs_init_fail rxy j I d

The same as `i_bs_init I I d` but may fail if the size in Arg0 is invalid.
Arg1 is not used.


i_bs_init_fail_heap
------------------------------
    i_bs_init_fail_heap I j I d

Follows the `i_fetch d d` that loads binary data size into __tmpA__. Allocates
space for a shared binary data of __tmpA__ size. Creates a ProcBin referencing
the data. Makes sure that heap has enough space for a subbinary and Arg0 more
words. Arg2 is Live. Puts the ProcBin to Arg3.


i_bs_init_heap
------------------------------
    i_bs_init_heap I I I d

Allocates space for a shared binary data of Arg0 size. Create a ProcBin
referencing the data. Makes sure that the heap has enough space for a subbinary
and Arg1 more words. Arg2 is Live. Puts the ProcBin into Arg3.


i_bs_init_heap_bin
------------------------------
    i_bs_init_heap_bin I I d

Allocates a heap binary of size Arg0 and makes sure that the heap has enough
space for a subbinary. Arg1 is Live. The heap binary is put to Arg2.


i_bs_init_heap_bin_heap
------------------------------
    i_bs_init_heap_bin_heap I I I d

Allocates a heap binary of size Arg0 and makes sure that the heap has enough
space for a subbinary and Arg1 more words. Arg2 is Live. The heap binary is put
to Arg3.


i_bs_init_writable
------------------------------
    i_bs_init_writable

Allocates a shared data space of size R0. Creates a ProcBin on the heap
referencing the data. Create a subbinary referencing the ProcBin. Save the
subbinary to R0.


i_bsl
------------------------------
    i_bsl j I d

Arg2 = __tmpA__ `<</>>` __tmpB__. The direction of the shift depends on the
sign of __tmpB__. Arg1 is Live. Jumps to Arg0 on error if Arg0 is not zero.


i_bs_match_string
------------------------------
    i_bs_match_string rx f I I

Compares Arg2 bits from the matching context Arg2 with the data referenced by
the raw data pointer Arg3. Jumps to the label Arg1 if there is no match.


i_bs_private_append
------------------------------
    i_bs_private_append j I d

Same as `i_bs_append j I I I d` but assumes that the binary writable.
Reallocates the shared data if there is not enough space. This should be safe.
Changes the subbinary __tmpB__ in place. No heap allocations. Arg1 is the unit.
Save the result to Arg2.


i_bs_put_utf16
------------------------------
    i_bs_put_utf16 j I s

Assumes that previous instructions created a binary creation context. Packs a
UTF-16 character Arg2 into the context. Arg1 are flags. The failure label Arg0
is unused.


i_bs_put_utf8
------------------------------
    i_bs_put_utf8 j s

Assumes that previous instructions created a binary creation context. Packs a
UTF-8 character Arg1 into the context. The failure label Arg0 is unused.


i_bsr
------------------------------
    i_bsr j I d

Arg2 = __tmpA__ `<</>>` __tmpB__. The direction of the shift depends on the
sign of __tmpB__. Arg1 is Live. Jumps to Arg0 on error if Arg0 is not zero.


i_bs_restore2
------------------------------
    i_bs_restore2 rx I

Does the opposite of `i_bs_save2 rx I`.  Restores the offset of the matching
context Arg0 from the saved offsets array at index Arg1.


i_bs_save2
------------------------------
    i_bs_save2 rx I

Saves the offset from the matching context Arg0 to the saved offsets array at
the index Arg1.


i_bs_skip_bits2
------------------------------
    i_bs_skip_bits2 f rx rxy I

Skips2 Arg2 units of the matching context Arg1. Arg3 is the unit size. Jumps to
Arg0 on failure.


i_bs_skip_bits2_imm2
------------------------------
    i_bs_skip_bits2_imm2 f rx I

Move the offset of the matching context Arg1 by Arg2 bits. Jumps to Arg0 on
failure.


i_bs_skip_bits_all2
------------------------------
    i_bs_skip_bits_all2 f rx I

Skips all remaining bits of the matching context Arg1. The number of bits
skipped should be divisible by unit Arg2. Jumps to the label Arg0 on failure.


i_bs_start_match2
------------------------------
    i_bs_start_match2 rxy f I I d

Checks that Arg0 is the matching context with enough slots for saved offsets.
The number of slots needed is given by Arg3. If there not enough slots of if
Arg0 is a regular binary then recreates the matching context and saves it to
Arg4. If something does not work jumps to Arg1. Arg2 is Live.


i_bs_utf16_size
------------------------------
    i_bs_utf16_size s d

    /*
      * Calculate the number of bytes needed to encode the source
      * operarand to UTF-16. If the source operand is invalid (e.g. wrong
      * type or range) we return a nonsense integer result (2 or 4). We
      * can get away with that because we KNOW that bs_put_utf16 will do
      * full error checking
      */


i_bs_utf8_size
------------------------------
    i_bs_utf8_size s d

    /*
      * Calculate the number of bytes needed to encode the source
      * operarand to UTF-8. If the source operand is invalid (e.g. wrong
      * type or range) we return a nonsense integer result (2 or 4). We
      * can get away with that because we KNOW that bs_put_utf16 will do
      * full error checking.
      */


i_bs_validate_unicode
------------------------------
    i_bs_validate_unicode j s

Validates a single unicode character Arg1. Raises badarg exception on error.
Arg0 is not used. NB: the existence of the instruction may be dependent on the
implementation detail of binary construction; see comment in beam_emu.c, line
3963.


i_bs_validate_unicode_retract
------------------------------
    i_bs_validate_unicode_retract j

Verifies that a matched out integer __tmpA__ falls into the valid range for
Unicode characters. If not the matching context __tmpB__ is rectracted by 32
bits. Arg0 looks like a failure label but it is never used.


i_bxor
------------------------------
    i_bxor j I d

Arg2 = __tmpA__ ^ __tmpB__. Arg1 is Live. Jumps to Arg0 on error if Arg0 is not
zero.


i_call
------------------------------
    i_call f

Sets __CP__ to the location after the instruction and then jumps to the label
Arg0.


i_call_ext
------------------------------
    i_call_ext e

Sets __CP__ to the point after the instruction and then jumps to the address of
the export entry Arg0.


i_call_ext_last
------------------------------
    i_call_ext_last e P

Restores __CP__ from the stack, drops Arg1 slots from the stack, and then jumps
to the address of the export entry Arg0.


i_call_ext_only
------------------------------
    i_call_ext_only e

Jumps to the address of the export entry Arg0.


i_call_fun
------------------------------
    i_call_fun I

Calls the fun with the arity Arg0. The fun is found in the arity'th registers.
Thus the fun call arguments are in registers starting with R0 and the fun
itself immediately follows. The result is returned in R0. Sets __CP__ to the
point after the instruction and jumps to the fun's entry.


i_call_fun_last
------------------------------
    i_call_fun_last I P

Same as `i_call_fun I` but restores __CP__ from stack and drops Arg1 slots from
it before proceeding to the fun's entry.


i_call_last
------------------------------
    i_call_last f P

Restores __CP__ from the stack, drops Arg1 slots from stack, and jumps to the
label Arg0.


i_call_only
------------------------------
    i_call_only f

Jumps to Arg0.


i_element
------------------------------
    i_element rxy j s d

Gets the Arg2'th element of the tuple Arg0 and places it to Arg3. Arg1 is
effectively disregarded.


i_fadd
------------------------------
    i_fadd l l l

Arg2 = Arg0 + Arg1.


i_fast_element
------------------------------
    i_fast_element rxy j I d

Gets the Arg2'th element of the tuple Arg0 and places it to Arg3. Arg1 is
effectively disregarded.


i_fcheckerror
------------------------------
    i_fcheckerror

Checks if the FR0 contains Nan or +-Inf. Raises badarith exception if this is
the case.


i_fdiv
------------------------------
    i_fdiv l l l

Arg2 = Arg0 / Arg1.


if_end
------------------------------
    if_end

Raises a if_clause exception.


i_fetch
------------------------------
    i_fetch s s

Fetches values from Arg0 and Arg1 and places them in __tmpA__ and __tmpB__
respectively.


i_fmul
------------------------------
    i_fmul l l l

Arg2 = Arg0 * Arg1.


i_fnegate
------------------------------
    i_fnegate l l l

Arg1 = -Arg0.


i_fsub
------------------------------
    i_fsub l l l

Arg2 = Arg0 - Arg1.


i_func_info
------------------------------
    i_func_info I a a I

Raises __function_clause__ exception. Arg1, Arg2, Arg3 are MFA. Arg0 is
a mystery coming out of nowhere, probably, needed for NIFs.


i_gc_bif1
------------------------------
    i_gc_bif1 j I s I d

Executes a guard BIF at the address Arg1 with a single parameter Arg2. Arg3 is
Live. Stores the result in Arg4. Jumps to Arg0 on error if it is not zero.
Otherwise, raises an exception.


i_gc_bif2
------------------------------
    i_gc_bif2 j I I d

Executes a guard BIF at the address Arg1 with two parameters - __tmpA__ and
__tmpB__. Arg2 is Live. Stores the result in Arg3. Jumps to Arg0 on error if it
is not zero.  Otherwise, raises an exception.


i_gc_bif3
------------------------------
    i_gc_bif3 j I s I d

Executes a guard BIF at the address Arg1 with three parameters - Arg2,
__tmpA__, and __tmpB__. Arg3 is Live. Stores the result in Arg4. Jumps to Arg0
on error if it is not zero.  Otherwise, raises an exception.


i_get
------------------------------
    i_get s d

Reads the process dictionary key Arg0 and places the result to Arg1.


i_get_tuple_element
------------------------------
    i_get_tuple_element rxy P rxy

Gets the value of the the Arg1'th element of the tuple Arg0 and puts it to
Arg2.  Arg1 is 1-based.


i_hibernate
------------------------------
    i_hibernate

Puts the process into a hibernated state dropping its stack and minimizing its
heap. When a message arrives or if the message queue is not empty the process
is waken up and starts executing a function identified by R0 (module), R1
(function), and R2 (arguments).


i_increment
------------------------------
    i_increment rxy I I d

Arg3 = Arg0 + Arg1. Arg2 is Live.


i_int_bnot
------------------------------
    i_int_bnot j s I d

Arg3 = ~ Arg1. Arg2 is Live. Jumps to Arg0 on error if Arg0 is not zero.


i_int_div
------------------------------
    i_int_div j I d

Arg2 = __tmpA__ / __tmpB__. Division is integer. Arg1 is Live. Jumps to Arg0 on
error if Arg0 is not zero.


i_is_eq
------------------------------
    i_is_eq f

Checks if __tmpA__ is equal to __tmpB__. Jumps to the label Arg0 if it is not.


i_is_eq_exact
------------------------------
    i_is_eq_exact f

Checks if __tmpA__ 'exactly' equals __tmpB__. Jumps to the label Arg0 if it
does not.


i_is_eq_exact_immed
------------------------------
    i_is_eq_exact_immed f rxy c

Checks if Arg1 equals Arg2 using _bitwise_ comparison. Jumps to Arg0 if it
does not.


i_is_eq_exact_literal
------------------------------
    i_is_eq_exact_literal f rxy c

Checks if Arg1 equals Arg2 using the term comparison. Jumps to Arg0 if it does
not.


i_is_ge
------------------------------
    i_is_ge f

Checks if __tmpA__ is greater than or equal to __tmpB__. Jumps to the label
Arg0 if it is not.


i_is_lt
------------------------------
    i_is_lt f

Checks if __tmpA__ is less than __tmpB__. Jumps to the label Arg0 if it is not.


i_is_ne
------------------------------
    i_is_ne f

Checks if __tmpA__ is equal to __tmpB__. Jumps to the label Arg0 if it is.


i_is_ne_exact
------------------------------
    i_is_ne_exact f

Checks if __tmpA__ 'exactly' equals __tmpB__. Jumps to the label Arg0 if it
does.


i_is_ne_exact_immed
------------------------------
    i_is_ne_exact_immed f rxy c

Checks if Arg1 equals Arg2 using _bitwise_ comparison. Jumps to Arg0 if it
does.


i_is_ne_exact_literal
------------------------------
    i_is_ne_exact_literal f rxy c

Checks if Arg1 equals Arg2 using the term comparison. Jumps to Arg0 if it does.


i_jump_on_val
------------------------------
    i_jump_on_val rxy f I I

Implements a 'jump table'. Calculates the index by adding Arg0 to the minimum
value Arg2. Jumps to Arg1 if the index falls outside of the table boundaries.
Arg3 is the length of the jump table. Picks the label from the table using the
calculated index and jumps there.


i_jump_on_val_zero
------------------------------
    i_jump_on_val_zero rxy f I

Same as `i_jump_on_val rxy f I I` but the minimum value is assumed to be zero.


i_loop_rec
------------------------------
    i_loop_rec f r

Picks the next message from the message queue and places it in R0. If there are
no messages then jumps to Arg0 which points to `wait` or `wait_timeout`
instruction.


i_make_fun
------------------------------
    i_make_fun I t

Creates a fun and puts it to R0. Arg0 contains a reference to the entry of the
lamdba table of the module. Arg1 is the number of free variables. The values of
free variables are taken from registers starting with R0. Only these registers
are considered live. It means that Arg1 is Live also.


i_m_div
------------------------------
    i_m_div j I d

Arg2 = __tmpA__ / __tmpB__. Mixed. Arg1 is Live. Jumps to Arg0 on error if Arg0
is not zero.


i_minus
------------------------------
    i_minus j I d

Arg2 = __tmpA__ - __tmpB__. Arg1 is Live. Jumps to Arg0 on error if Arg0 is not
zero.


i_move_call
------------------------------
    i_move_call c r f

Combines `move c r` and `call f`.


i_move_call_ext
------------------------------
    i_move_call_ext c r e

Combines `move c r` with `i_call_ext e`.


i_move_call_ext_last
------------------------------
    i_move_call_ext_last e P c r

Combines `move c r` with `i_call_last e`.


i_move_call_ext_only
------------------------------
    i_move_call_ext_only e c r

Combines `move c r` with `i_call_only e`.


i_move_call_last
------------------------------
    i_move_call_last f P c r

Combines `move c r` and `call_last f P`.


i_move_call_only
------------------------------
    i_move_call_only f c r

Combines `move c r` and `call_only f`.


i_new_bs_put_binary
------------------------------
    i_new_bs_put_binary j s I s

Assumes that previous instructions created a binary creation context. Packs a
binary Arg3 of Arg1 units size into the context. Arg2 are flags and the unit.
The failure label Arg0 is not used.


i_new_bs_put_binary_all
------------------------------
    i_new_bs_put_binary_all j s I

Assumes that previous instructions created a binary creation context. Packs a
whole binary Arg1 into the context. Arg2 is the unit. The failure label Arg0 is
not used.


i_new_bs_put_binary_imm
------------------------------
    i_new_bs_put_binary_imm j I s

Assumes that previous instructions created a binary creation context. Packs a
binary Arg2 of Arg1 bits size into the context. The failure label Arg0 is not
used.


i_new_bs_put_float
------------------------------
    i_new_bs_put_float j s I s

Assumes that previous instructions created a binary creation context. Packs a
float of Arg1 units size into the context. Arg2 are the unit and flags. The
failure label Arg0 is not used.


i_new_bs_put_float_imm
------------------------------
    i_new_bs_put_float_imm j I I s

Assumes that previous instructions created a binary creation context. Packs a
float Arg3 of Arg1 bits size into the context. Arg2 are flags. The failure
label Arg0 is not used.


i_new_bs_put_integer
------------------------------
    i_new_bs_put_integer j s I s

Assumes that previous instructions created a binary creation context. Packs an
integer value Arg3 into Arg1 units of the context. Arg2 are the unit and flags.
The failure label Arg0 is unused.


i_new_bs_put_integer_imm
------------------------------
    i_new_bs_put_integer_imm j I I s

Assumes that previous instructions created a binary creation context. Packs an
integer value Arg3 into Arg1 bits of the context. Arg2 are flags.  The failure
label Arg0 is unused.


init
------------------------------
    init y

Sets the Arg0 slot to nil. The op was called 'kill' earlier.


init2
------------------------------
    init2 y y

Sets slots Arg0 and Arg1 to nil.


init3
------------------------------
    init3 y y y

Sets slots Arg0, Arg1, and Arg2 to nil.


int_code_end
------------------------------
<div class="meta">Meta

    int_code_end

Maybe marks the end of the code.


i_plus
------------------------------
    i_plus j I d

Arg2 = __tmpA__ + __tmpB__. Arg1 is Live. Jumps to Arg0 on error if Arg0 is not
zero.


i_put_tuple
------------------------------
    i_put_tuple rxy I

Creates a tuple on the heap and places it in Arg0. Arg1 is the arity of the
tuple. The elements of the tuple follow the instruction. Some of the elements
may refer to registers or stack slots.


i_recv_set
------------------------------
    i_recv_set f

Sets the __SAVE__ pointer to the saved last pointer if the label is right. This
is somehow needed for in-order processing of monitoring messages.


i_rem
------------------------------
    i_rem j I d

Arg2 = __tmpA__ % __tmpB__. Division is integer. Arg1 is Live. Jumps to Arg0 on
error if Arg0 is not zero.


is_atom
------------------------------
    is_atom f rxy

Jumps to the label Arg0 if Arg1 is not an atom.


is_bitstring
------------------------------
    is_bitstring f rxy

Jumps to the label Arg0 if Arg1 is not a bitstring (or a binary).


is_boolean
------------------------------
    is_boolean f rxy

Jumps to the label Arg0 if Arg1 is not true or false.


i_select_tuple_arity
------------------------------
    i_select_tuple_arity r f I
    i_select_tuple_arity x f I
    i_select_tuple_arity y f I

Checks that Arg0 is tuple and then searches the array for {arity,addr} for the
right arity. See `i_select_val rxy f I`.


i_select_tuple_arity2
------------------------------
    i_select_tuple_arity2 r f A f A f
    i_select_tuple_arity2 x f A f A f
    i_select_tuple_arity2 y f A f A f

Same as `i_select_tuple_arity rxy f I` but uses the array made up of two pairs:
{Arg2,Arg3} and {Arg4,Arg5}.


i_select_val
------------------------------
    i_select_val r f I<br>
    i_select_val x f I<br>
    i_select_val y f I

Searches an array of {val,addr} pairs for the value of Arg0. The length of the
array is Arg2. If the value is found the execution continues at the
corresponding _addr_. Otherwise, jumps to Arg1. Uses binary search and
_bitwise_ comparisons.


i_select_val2
------------------------------
    i_select_val2 r f c f c f
    i_select_val2 x f c f c f
    i_select_val2 y f c f c f

Same as `i_select_val rxy f I` but uses an array made of {Arg2,Arg3} and
{Arg4,Arg5}.


is_float
------------------------------
    is_float f rxy

Jumps to the label Arg0 if Arg1 is not a float.


is_function
------------------------------
    is_function f rxy

Jumps to the label Arg0 if Arg1 is not a fun.


is_function2
------------------------------
    is_function2 f s s

Jumps to the label Arg0 if Arg1 is not fun or have an arity different from
Arg1.


is_integer
------------------------------
    is_integer f rxy

Jumps to the label Arg0 if Arg1 is not integer.


is_integer_allocate
------------------------------
    is_integer_allocate f rx I I

Combines `is_integer f rx` and `allocate I I`.


is_list
------------------------------
    is_list f rxy

Jumps to the label Arg0 if Arg1 is not a list.


is_nil
------------------------------
    is_nil f rxy

Jumps to the label Arg0 if Arg1 is not nil.


is_nonempty_list
------------------------------
    is_nonempty_list f rxy

Jumps to the label Arg0 if Arg1 is not an nonempty list.


is_nonempty_list_allocate
------------------------------
    is_nonempty_list_allocate f rx I t

Combines `is_nonempty_list f rx` and `allocate I t`.


is_nonempty_list_test_heap
------------------------------
    is_nonempty_list_test_heap f r I t

Combines `is_nonempty_list f r` and `test_heap I t`.


is_number
------------------------------
    is_number f rxy

Jumps to Arg0 if Arg1 is not integer and is not float.


is_pid
------------------------------
    is_pid f rxy

Jumps to the label Arg0 if Arg1 is not a pid.


is_port
------------------------------
    is_port f rxy

Jumps to the label Arg0 if Arg1 is not a port.


is_reference
------------------------------
    is_reference f rxy

Jumps to the label Arg0 if Arg1 is not a reference.


is_tuple
------------------------------
    is_tuple f rxy

Jumps to the label Arg0 if Arg1 is not a tuple.


is_tuple_of_arity
------------------------------
    is_tuple_of_arity f rxy A

Jumps to the label Arg0 if Arg1 is not a tuple or its arity is not Arg2. If
Arg1 is tuple its value is saved to __tmpA__.


i_times
------------------------------
    i_times j I d

Arg2 = __tmpA__ * __tmpB__. Mixed. Arg1 is Live. Jumps to Arg0 on error if Arg0
is not zero.


i_trim
------------------------------
    i_trim I

Removes Arg0 slots from the stack. The saved __CP__ is moved to the new top of
the stack.


i_wait_error
------------------------------
    i_wait_error

Raises a timeout_value exception.


i_wait_error_locked
------------------------------
    i_wait_error_locked

Same as `i_wait_error` but with due respect to SMP.


i_wait_timeout
------------------------------
    i_wait_timeout f I
    i_wait_timeout f s

Sets the timer to the appropriate time as indicated by Arg1. Afterwards acts as
`wait f`.


i_wait_timeout_locked
------------------------------
    i_wait_timeout_locked f I
    i_wait_timeout_locked f s

Same as `i_wait_timeout f I` but with SMP trickery.


jump
------------------------------
    jump f

Continues execution at the location Arg0.


label
------------------------------
    label L

The label L is set to the current code location.


line
------------------------------
    line I

Maybe augments debugging output when backtracking.


loop_rec_end
------------------------------
    loop_rec_end f

Advances the __SAVE__ pointer to the next message as the current message did
not match. Jumps to Arg0 that points to `loop_rec f r` instruction.


move
------------------------------
    move rxync rxy

Copies Arg0 to Arg1.


move2
------------------------------
    move2 x y x y
    move2 y x y x
    move2 x x x x

Combine two move operations.


move_call
------------------------------
    move_call xy r f

Same as `i_move_call xy r f`.


move_call_last
------------------------------
    move_call_last xy r f Q

Same as `i_move_last f Q xy r`.


move_call_only
------------------------------
    move_call_only x r f

Same as `i_move_only xy r f`.


move_deallocate_return
------------------------------
    move_deallocate_return xycn r Q

Combines `move xycn r`, `deallocate Q`, and `return`.


move_jump
------------------------------
    move_jump f ncxy

Move the value from Arg1 to R0 and then jumps to the label Arg0.


move_return
------------------------------
    move_return xcn r

Combines `move xcn r` and `return`.


move_x1
------------------------------
    move_x1 c

Sets R1 to the value of Arg0.


move_x2
------------------------------
    move_x2 c

Sets R2 to the value of Arg0.


node
------------------------------
    node rxy

Put the node identifier of the virtual machine to Arg0.


put_list
------------------------------
    put_list s s d

Create a cons cell on the heap and places in onto Arg2. Arg0 is the head of the
list saved to __HTOP__[0] and Arg1 is the tail saved to __HTOP__[1].


raise
------------------------------
    raise s s

Raises the exception. The instruction is garbled by backward compatibility.
Arg0 is a stack trace and Arg1 is the value accompanying the exception. The
reason of the raised exception is dug up from the stack trace.


recv_mark
------------------------------
    recv_mark f

Saves the last pointer of the message queue and the label of the soon expected
`loop_rec f r`.


remove_message
------------------------------
    remove_message

Removes the (matched) message from the message queue.


return
------------------------------
    return

__IP__ is set to __CP__.


self
------------------------------
    self rxy

Put the identifier of the current process to Arg0.


send
------------------------------
    send

Sends the message from R1 to the process R0.


set_tuple_element
------------------------------
    set_tuple_element s d P

Sets the Arg2'th element of the tuple Arg1 to to the value of Arg0. The index
in Arg2 is 1-based.


system_limit
------------------------------
    system_limit j

Similar to `badarg j` but raises `system_limit` exception.


test_arity
------------------------------
    test_arity f rxy A

Jumps to the label Arg0 is the arity of the tuple Arg1 is not Arg2. The value
of Arg1 is saved to __tmpA__.


test_heap
------------------------------
    test_heap I t

Ensures that the heap has at least Arg0 words available. Arg1 is Live.


test_heap_1_put_list
------------------------------
    test_heap_1_put_list I y

Test that the heap has a room for Arg0 words and than conses value of Arg1 with
R0.


timeout
------------------------------
    timeout

Timeout has occured. Resets the __SAVE__ pointer to the first message in the
message queue.


timeout_locked
------------------------------
    timeout_locked

Same as `timeout` but with SMP precautions.


try_case_end
------------------------------
    try_case_end s

Raises a `try_clause` exception with the value read from Arg0.


try_end
------------------------------
    try_end y

Pops a 'catch' context. Erases the label saved in the Arg0 slot. Noval in R0
indicate that something is caught. If so, R0 is set to R1, R1 - to R2, R2 - to
R3.


wait
------------------------------
    wait f

Prepares to wait indefinitely for a message to arrive. When the message arrives
transfers control to the `loop_rec` instruction at the label Arg0.


wait_locked
------------------------------
    wait_locked f

Same as `wait f`.


wait_unlocked
------------------------------
    wait_unlocked f

Same as `wait f` but messes with SMP locks.
