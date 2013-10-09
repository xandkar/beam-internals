BEAM Instruction Set [1]
========================

Source: http://erlangonxen.org/more/beam


allocate
------------------------------


<div class="args">allocate t t</div>

Allocates Arg0 slots on the stack. Arg1 is Live.


allocate_heap
------------------------------


<div class="args">allocate_heap t I t</div>

Allocates Arg0 slots on the stack. See <span class="see" data-id="allocate">allocate t
t</span>. Ensures that heap contains at least Arg1 words after <b>HTOP</b>. Arg2 is
Live.


allocate_heap_zero
------------------------------


<div class="args">allocate_heap_zero t I t</div>

Same as <span class="see" data-id="allocate_heap">allocate_heap t I t</span> but sets the slots to nil.


allocate_init
------------------------------


<div class="args">allocate_init t I y</div>

Combines <span class="see" data-id="allocate">allocate t I</span>
 and <span class="see" data-id="init">init y</span>.


allocate_zero
------------------------------


<div class="args">allocate_zero t t</div>

Same as <span class="see" data-id="allocate">allocate t t</span> but sets the slots to nil.


apply
------------------------------


<div class="args">apply I</div>

Finds the address from the export entry for the function (possibly BIF)
identified by the module R(N), the function R(N+1), and the arity N. The arity
is taken from Arg0. Sets <b>CP</b> to the next instruction and jumps to the found
address.


apply_last
------------------------------


<div class="args">apply_last I P</div>

Similar to <span class="see" data-id="apply">apply I</span> but restores <b>CP</b>
from stack and drops Arg1 slots from it before jumping to the found address.


badarg
------------------------------


<div class="args">badarg j</div>

If Arg0 is not 0 then jumps to the label Arg0. Otherwise, raises the badarg exception.


badmatch
------------------------------


<div class="args">badmatch rxy</div>

Raises a badmatch exception with the value of Arg0.


bif1
------------------------------


<div class="args">bif1 f b s d</div>

Calls the BIF from Arg1 with the argument Arg2 and places the result to Arg3.
Upon error jumps to Arg0 as appropriate for the guard BIF.


bif1_body
------------------------------


<div class="args">bif1_body b s d</div>

Calls the BIF from Arg0 with the argument Argr1 and places the result to Arg3.
This is the case of a guard BIF in the function body. It fails like an ordinary
BIF.


bs_context_to_binary
------------------------------


<div class="args">bs_context_to_binary rxy</div>

Converts the matching context to a (sub)binary using almost the same code as
<span class="see" data-id="i_bs_get_binary_all_reuse">i_bs_get_binary_all_reuse rx f I</span>.


bs_put_string
------------------------------


<div class="args">bs_put_string I I</div>

Assumes that previous instructions created a binary creation context. Packs a
string of characters Arg0 bytes long referenced by the pointer Arg1 into the
context.


bs_test_tail_imm2
------------------------------


<div class="args">bs_test_tail_imm2 f rx I</div>

Checks that the matching context Arg1 has exactly Arg2 unmatched bits. Jumps to
the label Arg0 if it is not so.


bs_test_unit
------------------------------


<div class="args">bs_test_unit f rx I</div>

Checks that the size of the remainder of the matching context Arg1 is divisible
by unit Arg2. Jumps to the label Arg0 if it is not so.


bs_test_unit8
------------------------------


<div class="args">bs_test_unit8 f rx</div>

Checks that the size of the remainder of the matching context Arg1 is divisible
by 8. Jumps to the label Arg1 if it is not.


bs_test_zero_tail2
------------------------------


<div class="args">bs_test_zero_tail2 f rx</div>

Jumps to the label in Arg0 if the matching context Arg1 still have unmatched
bits.


call_bif0
------------------------------


<div class="args">call_bif0 e</div>

Calls the BIF from Arg0 without arguments and returns result in R0.


call_bif1
------------------------------


<div class="args">call_bif1 e</div>

Calls the BIF from Arg0 with R0 as the argument and returns result in R0.


call_bif2
------------------------------


<div class="args">call_bif2 e</div>

Calls the BIF from Arg0 with arguments in R0 and R1 and returns result in R0.


call_bif3
------------------------------


<div class="args">call_bif3 e</div>

Calls the BIF from Arg0 with arguments in R0, R1, and R2 and returns result in R0.


case_end
------------------------------


<div class="args">case_end rxy</div>

Raises a case_clause exception with the value of Arg0.


catch
------------------------------


<div class="args">catch y f</div>

Creates a new 'catch' context. Saves value of the label from Arg1 to the Arg0 stack
slot.


catch_end
------------------------------


<div class="args">catch_end y</div>

Pops a 'catch' context. Erases the label saved in the Arg0 slot. Noval in R0
indicates that something is caught. If R1 contains atom 'throw' then R0 is
set to R2. If R1 contains atom 'error' R0 is set to {'EXIT',{R2,&lt;stack
trace&gt;}}.


deallocate
------------------------------


<div class="args">deallocate I</div>

Restores <b>CP</b> to the value referenced by <b>EP</b>. Adds Arg0 + 1 to <b>EP</b> to
remove the saved <b>CP</b> and Arg0 slots from the stack.


deallocate_return
------------------------------


<div class="args">deallocate_return Q</div>

Combines <span class="see" data-id="deallocate">deallocate Q</span> and
<span class="see" data-id="return">return</span>.


extract_next_element
------------------------------


<div class="args">extract_next_element xy</div>

The pointer in <b>tmpA</b> moved to the next element of the tuple. The element is
read from the location pointed to by <b>tmpA</b> to Arg0.


extract_next_element2
------------------------------


<div class="args">extract_next_element2 xy</div>

The pointer in <b>tmpA</b> moved to the next element of the tuple. Copies 2 terms
from the array pointed to by <b>tmpA</b> to the registers or slots pointed to by
Arg0. For instance, if Arg0 is R3 then tuple elements are loaded to R3 and R4.


extract_next_element3
------------------------------


<div class="args">extract_next_element3 xy</div>

Same as <span class="see" data-id="extract_next_element2">extract_next_element2 xy</span> but copies three elements.


fclearerror
------------------------------


<div class="args">fclearerror</div>

Maybe clears FP error flag.


fconv
------------------------------


<div class="args">fconv d l</div>

Converts Arg0 to float and places the result to Arg1.


fmove
------------------------------


<div class="args">fmove qdl ld</div>

Copies Arg0 to Arg1.


get_list
------------------------------


<div class="args">get_list rxy rxy rxy</div>

Gets the head of the list from Arg0 and puts it to Arg1, the tail &ndash; to Arg2.


i_apply
------------------------------


<div class="args">i_apply</div>

Applies the function identified by R0 (module), R1 (function), and R2
(arguments). Sets <b>CP</b> to the point after the instruction.


i_apply_fun
------------------------------


<div class="args">i_apply_fun</div>

Applies the fun R0 to the argument list in R1. Set <b>CP</b> to the location right
after the instruction.


i_apply_fun_last
------------------------------


<div class="args">i_apply_fun_last P</div>

Applies the fun R0 to the argument list in R1. Restores <b>CP</b> from stack and
deallocates Arg0 slots from stack.


i_apply_fun_only
------------------------------


<div class="args">i_apply_fun_only</div>

Applies the fun R0 to the argument list in R1.


i_apply_last
------------------------------


<div class="args">i_apply_last P</div>

Applies the function identified by R0 (module), R1 (function), and R2
(arguments). Afterwards, restores <b>CP</b> from stack and deallocates Arg0 slots
from stack.


i_apply_only
------------------------------


<div class="args">i_apply_only</div>

Applies the function identified by R0 (module), R1 (function), and R2
(arguments).


i_band
------------------------------


<div class="args">i_band j I d</div>

Arg2 = <b>tmpA</b> & <b>tmpB</b>. Arg1 is Live. Jumps to Arg0 on error if Arg0 is not
zero.


i_bif2
------------------------------


<div class="args">i_bif2 f b d</div>

Calls the guard BIF from Arg1 with the two arguments in <b>tmpA</b> and <b>tmpB</b> and
places the result to Arg2. Upon error jumps to Arg0 as appropriate for a guard
BIF.


i_bif2_body
------------------------------


<div class="args">i_bif2_body b d</div>

Calls the guard BIF from Arg0 with the two arguments in <b>tmpA</b> and <b>tmpB</b> and
places the result to Arg1. This is the case of a guard BIF in the function body.
It fails like an ordinary BIF.


i_bor
------------------------------


<div class="args">i_bor j I d</div>

Arg2 = <b>tmpA</b> | <b>tmpB</b>. Arg1 is Live. Jumps to Arg0 on error if Arg0 is not
zero.


i_bs_add
------------------------------


<div class="args">i_bs_add j I d</div>

Calculates the total of the number of bits in <b>tmpA</b> and the number of units in
<b>tmpB</b>. Arg1 is the unit. Stores the result to Arg2.


i_bs_append
------------------------------


<div class="args">i_bs_append j I I I d</div>

Appends <b>tmpA</b> bits to a binary <b>tmpB</b>. If the binary is a writable subbinary
referencing a ProcBin with enough empty space then a new writable subbinary is
created and the old one is made non-writable. In other cases, creates a new
shared data, a new ProcBin, and a new subbinary. For all heap allocation, a
space for more Arg1 words are requested. Arg2 is Live. Arg3 is unit. Saves the
resultant subbinary to Arg4.


i_bs_get_binary2
------------------------------


<div class="args">i_bs_get_binary2 f rx I s I d</div>

Gets a binary from the matching context Arg1 of size (in units) Arg3. Arg2 is
Live. Arg4 are flags and unit. Puts result to Arg5. Jumps to Arg0 on failure.


i_bs_get_binary_all2
------------------------------


<div class="args">i_bs_get_binary_all2 f rx I I d</div>

Gets the rest of the matching context Arg1 as a binary and puts it to Arg4. The
binary size should be divisable by unit Arg3. Arg2 is Live. Jumps to Arg0 upon
failure.


i_bs_get_binary_all_reuse
------------------------------


<div class="args">i_bs_get_binary_all_reuse rx f I</div>

Replaces the matching context Arg0 with the rest of its reminder represented as
a binary. Arg2 is the unit. The size of the binary should be divisible by unit.
Jumps to the label Arg1 on failure.


i_bs_get_binary_imm2
------------------------------


<div class="args">i_bs_get_binary_imm2 f rx I I I d</div>

Gets a binary from the matching context Arg1 of size (in bits) Arg3. Arg2 is
Live. Arg4 are flags. The binary is put to Arg5. Jumps yo Arg0 on failure.


i_bs_get_float2
------------------------------


<div class="args">i_bs_get_float2 f rx I s I d</div>

Gets the float value form the matching context Arg1. Arg3 is the size in units.
Arg4 are unit and flags. Puts the value to Arg5. Arg2 is Live. Jumps to Arg0 on
failure.


i_bs_get_integer
------------------------------


<div class="args">i_bs_get_integer f I I d</div>

Gets an integer of size <b>tmpB</b> (in units) from the matching context <b>tmpA</b> and
saves it to Arg3. Arg1 is Live.  Arg2 are flags and unit. Jumps to Arg0 on
failure.


i_bs_get_integer_16
------------------------------


<div class="args">i_bs_get_integer_16 rx f d</div>

Gets an 16-bit integer from the matching context Arg0 and saves it to Arg2. Jumps
to Arg1 if there are not enough bits left.


i_bs_get_integer_32
------------------------------


<div class="args">i_bs_get_integer_32 rx f I d</div>

Gets an 32-bit integer from the matching context Arg0 and saves it to Arg3. Jumps
to Arg1 if there are not enough bits left. Arg2 is Live as the integer may not
be small.


i_bs_get_integer_8
------------------------------


<div class="args">i_bs_get_integer_8 rx f d</div>

Gets an 8-bit integer from the matching context Arg0 and saves it to Arg2. Jumps
to Arg1 if there are not enough bits left.


i_bs_get_integer_imm
------------------------------


<div class="args">i_bs_get_integer_imm rx I I f I d</div>

Gets an integer of size (in bits) Arg1 from the matching context Arg0 and puts
it to Arg5. Arg4 are flags. Arg2 is Live. Jumps to the label Arg3 on failure.


i_bs_get_integer_small_imm
------------------------------


<div class="args">i_bs_get_integer_small_imm rx I f I d</div>

Gets a (small) integer of size (in bits) Arg1 from the matching context Arg0 and
puts it to Arg4. Arg3 are flags. Jumps to the label Arg2 on failure.


i_bs_get_utf16
------------------------------


<div class="args">i_bs_get_utf16 rx f I d</div>

Extracts a UTF-16 encoded character from the matching context Arg0 using flags
Arg2 and places it to Arg3. Jumps to Arg1 upon failure.


i_bs_get_utf8
------------------------------


<div class="args">i_bs_get_utf8 rx f d</div>

Extracts a UTF-8 encoded character from the matching context Arg0 and places it
to Arg2. Jumps to Arg1 upon failure.


i_bs_init
------------------------------


<div class="args">i_bs_init I I d</div>

Allocates space for a shared binary data of Arg0 size. Creates a ProcBin
referencing the data. Makes sure that the heap has enough space for a subbinary.
Arg1 is Live. Puts the ProcBin into Arg2.


i_bs_init_bits
------------------------------


<div class="args">i_bs_init_bits I I d</div>

Same as <span class="see" data-id="i_bs_init_bits_heap">i_bs_init_bits_heap I I I d</span>
 but the number of extra words allocated on heap is zero.


i_bs_init_bits_fail
------------------------------


<div class="args">i_bs_init_bits_fail rxy j I d</div>

Same as <span class="see" data-id="i_bs_init_bits_heap">i_bs_init_bits_heap I I I d</span>
but the number of extra words allocated on the heap is zero and may fail if the
number of bits in Arg0 is not valid. Arg1 is not used.


i_bs_init_bits_fail_heap
------------------------------


<div class="args">i_bs_init_bits_fail_heap I j I d</div>

Same as <span class="see" data-id="i_bs_init_bits_heap">i_bs_init_bits_heap I I I d</span>
 but the number of bits is fetched to <b>tmpA</b> by previous instruction and
may fail if the number of bits in <b>tmpA</b> is not valid. Arg1 is not used.


i_bs_init_bits_heap
------------------------------


<div class="args">i_bs_init_bits_heap I I I d</div>

Allocates a heap binary of size (in bits) Arg0. If the size is not divisible by
8 than allocates a subbinary referencing the exact number of bits of the heap
binary. Makes sure that heap has Arg1 extra words available. Arg2 is Live. Puts
the result (the heap binary or the subbinary) to Arg3.


i_bs_init_fail
------------------------------


<div class="args">i_bs_init_fail rxy j I d</div>

The same as <span class="see" data-id="i_bs_init">i_bs_init I I d</span> but may fail if the size in Arg0 is invalid.
Arg1 is not used.


i_bs_init_fail_heap
------------------------------


<div class="args">i_bs_init_fail_heap I j I d</div>

Follows the <span class="see" data-id="i_fetch">i_fetch d d</span> that loads binary data
size into <b>tmpA</b>. Allocates space for a shared binary data of <b>tmpA</b>
size. Creates a ProcBin referencing the data. Makes sure that heap has enough
space for a subbinary and Arg0 more words. Arg2 is Live. Puts the ProcBin to
Arg3.


i_bs_init_heap
------------------------------


<div class="args">i_bs_init_heap I I I d</div>

Allocates space for a shared binary data of Arg0 size. Create a ProcBin
referencing the data. Makes sure that the heap has enough space for a subbinary
and Arg1 more words. Arg2 is Live. Puts the ProcBin into Arg3.


i_bs_init_heap_bin
------------------------------


<div class="args">i_bs_init_heap_bin I I d</div>

Allocates a heap binary of size Arg0 and makes sure that the heap has enough
space for a subbinary. Arg1 is Live. The heap binary is put to Arg2.


i_bs_init_heap_bin_heap
------------------------------


<div class="args">i_bs_init_heap_bin_heap I I I d</div>

Allocates a heap binary of size Arg0 and makes sure that the heap has enough
space for a subbinary and Arg1 more words. Arg2 is Live. The heap binary is put
to Arg3.


i_bs_init_writable
------------------------------


<div class="args">i_bs_init_writable</div>

Allocates a shared data space of size R0. Creates a ProcBin on the heap
referencing the data. Create a subbinary referencing the ProcBin. Save the
subbinary to R0.


i_bsl
------------------------------


<div class="args">i_bsl j I d</div>

Arg2 = <b>tmpA</b> &lt;&lt;/&gt;&gt; <b>tmpB</b>. The direction of the shift depends on the sign of
<b>tmpB</b>. Arg1 is Live. Jumps to Arg0 on error if Arg0 is not zero.


i_bs_match_string
------------------------------


<div class="args">i_bs_match_string rx f I I</div>

Compares Arg2 bits from the matching context Arg2 with the data referenced by
the raw data pointer Arg3. Jumps to the label Arg1 if there is no match.


i_bs_private_append
------------------------------


<div class="args">i_bs_private_append j I d</div>

Same as <span class="see" data-id="i_bs_append">i_bs_append j I I I d</span> but assumes
that the binary writable.  Reallocates the shared data if there is not enough
space. This should be safe.  Changes the subbinary <b>tmpB</b> in place. No heap
allocations. Arg1 is the unit.  Save the result to Arg2.


i_bs_put_utf16
------------------------------


<div class="args">i_bs_put_utf16 j I s</div>

Assumes that previous instructions created a binary creation context. Packs a
UTF-16 character Arg2 into the context. Arg1 are flags. The failure label Arg0
is unused.


i_bs_put_utf8
------------------------------


<div class="args">i_bs_put_utf8 j s</div>

Assumes that previous instructions created a binary creation context. Packs a
UTF-8 character Arg1 into the context. The failure label Arg0 is unused.


i_bsr
------------------------------


<div class="args">i_bsr j I d</div>

Arg2 = <b>tmpA</b> &gt;&gt;/&lt;&lt; <b>tmpB</b>. The direction of the shift depends on the sign of
<b>tmpB</b>. Arg1 is Live. Jumps to Arg0 on error if Arg0 is not zero.


i_bs_restore2
------------------------------


<div class="args">i_bs_restore2 rx I</div>

Does the opposite of <span class="see" data-id="i_bs_save2">i_bs_save2 rx I</span>.
Restores the offset of the matching context Arg0 from the saved offsets array at index Arg1.


i_bs_save2
------------------------------


<div class="args">i_bs_save2 rx I</div>

Saves the offset from the matching context Arg0 to the saved offsets array at
the index Arg1.


i_bs_skip_bits2
------------------------------


<div class="args">i_bs_skip_bits2 f rx rxy I</div>

Skips2 Arg2 units of the matching context Arg1. Arg3 is the unit size. Jumps to
Arg0 on failure.


i_bs_skip_bits2_imm2
------------------------------


<div class="args">i_bs_skip_bits2_imm2 f rx I</div>

Move the offset of the matching context Arg1 by Arg2 bits. Jumps to Arg0 on
failure.


i_bs_skip_bits_all2
------------------------------


<div class="args">i_bs_skip_bits_all2 f rx I</div>

Skips all remaining bits of the matching context Arg1. The number of bits
skipped should be divisible by unit Arg2. Jumps to the label Arg0 on failure.


i_bs_start_match2
------------------------------


<div class="args">i_bs_start_match2 rxy f I I d</div>

Checks that Arg0 is the matching context with enough slots for saved offsets.
The number of slots needed is given by Arg3. If there not enough slots of if
Arg0 is a regular binary then recreates the matching context and saves it to
Arg4. If something does not work jumps to Arg1. Arg2 is Live.


i_bs_utf16_size
------------------------------


<div class="args">i_bs_utf16_size s d</div>

<pre>
/*
  * Calculate the number of bytes needed to encode the source
  * operarand to UTF-16. If the source operand is invalid (e.g. wrong
  * type or range) we return a nonsense integer result (2 or 4). We
  * can get away with that because we KNOW that bs_put_utf16 will do
  * full error checking
  */
</pre>


i_bs_utf8_size
------------------------------


<div class="args">i_bs_utf8_size s d</div>

<pre>
/*
  * Calculate the number of bytes needed to encode the source
  * operarand to UTF-8. If the source operand is invalid (e.g. wrong
  * type or range) we return a nonsense integer result (2 or 4). We
  * can get away with that because we KNOW that bs_put_utf16 will do
  * full error checking.
  */
</pre>


i_bs_validate_unicode
------------------------------


<div class="args">i_bs_validate_unicode j s</div>

Validates a single unicode character Arg1. Raises badarg exception on error. Arg0
is not used. NB: the existence of the instruction may be dependent on the
implementation detail of binary construction; see comment in beam_emu.c, line
3963.


i_bs_validate_unicode_retract
------------------------------


<div class="args">i_bs_validate_unicode_retract j</div>

Verifies that a matched out integer <b>tmpA</b> falls into the valid range for
Unicode characters. If not the matching context <b>tmpB</b> is rectracted by 32
bits. Arg0 looks like a failure label but it is never used.


i_bxor
------------------------------


<div class="args">i_bxor j I d</div>

Arg2 = <b>tmpA</b> ^ <b>tmpB</b>. Arg1 is Live. Jumps to Arg0 on error if Arg0 is not
zero.


i_call
------------------------------


<div class="args">i_call f</div>

Sets <b>CP</b> to the location after the instruction and then jumps to the label
Arg0.


i_call_ext
------------------------------


<div class="args">i_call_ext e</div>

Sets <b>CP</b> to the point after the instruction and then jumps to the address of
the export entry Arg0.


i_call_ext_last
------------------------------


<div class="args">i_call_ext_last e P</div>

Restores <b>CP</b> from the stack, drops Arg1 slots from the stack, and then jumps
to the address of the export entry Arg0.


i_call_ext_only
------------------------------


<div class="args">i_call_ext_only e</div>

Jumps to the address of the export entry Arg0.


i_call_fun
------------------------------


<div class="args">i_call_fun I</div>

Calls the fun with the arity Arg0. The fun is found in the arity'th registers.
Thus the fun call arguments are in registers starting with R0 and the fun itself
immediately follows. The result is returned in R0. Sets <b>CP</b> to the point after
the instruction and jumps to the fun's entry.


i_call_fun_last
------------------------------


<div class="args">i_call_fun_last I P</div>

Same as <span class="see" data-id="i_call_fun">i_call_fun I</span> but restores <b>CP</b>
 from stack and drops Arg1 slots from it before proceeding to the fun's entry.


i_call_last
------------------------------


<div class="args">i_call_last f P</div>

Restores <b>CP</b> from the stack, drops Arg1 slots from stack, and jumps to the
label Arg0.


i_call_only
------------------------------


<div class="args">i_call_only f</div>

Jumps to Arg0.


i_element
------------------------------


<div class="args">i_element rxy j s d</div>

Gets the Arg2'th element of the tuple Arg0 and places it to Arg3. Arg1 is
effectively disregarded.


i_fadd
------------------------------


<div class="args">i_fadd l l l</div>

Arg2 = Arg0 + Arg1.


i_fast_element
------------------------------


<div class="args">i_fast_element rxy j I d</div>

Gets the Arg2'th element of the tuple Arg0 and places it to Arg3. Arg1 is
effectively disregarded.


i_fcheckerror
------------------------------


<div class="args">i_fcheckerror</div>

Checks if the FR0 contains Nan or +-Inf. Raises badarith exception if this is the
case.


i_fdiv
------------------------------


<div class="args">i_fdiv l l l</div>

Arg2 = Arg0 / Arg1.


if_end
------------------------------


<div class="args">if_end</div>

Raises a if_clause exception.


i_fetch
------------------------------


<div class="args">i_fetch s s</div>

Fetches values from Arg0 and Arg1 and places them in <b>tmpA</b> and <b>tmpB</b>
respectively.


i_fmul
------------------------------


<div class="args">i_fmul l l l</div>

Arg2 = Arg0 * Arg1.


i_fnegate
------------------------------


<div class="args">i_fnegate l l l</div>

Arg1 = -Arg0.


i_fsub
------------------------------


<div class="args">i_fsub l l l</div>

Arg2 = Arg0 - Arg1.


i_func_info
------------------------------


<div class="args">i_func_info I a a I</div>

Raises <b>function_clause</b> exception. Arg1, Arg2, Arg3 are MFA. Arg0 is
a mystery coming out of nowhere, probably, needed for NIFs.


i_gc_bif1
------------------------------


<div class="args">i_gc_bif1 j I s I d</div>

Executes a guard BIF at the address Arg1 with a single parameter Arg2. Arg3 is
Live. Stores the result in Arg4. Jumps to Arg0 on error if it is not zero.
Otherwise, raises an exception.


i_gc_bif2
------------------------------


<div class="args">i_gc_bif2 j I I d</div>

Executes a guard BIF at the address Arg1 with two parameters &ndash; <b>tmpA</b> and
<b>tmpB</b>. Arg2 is Live. Stores the result in Arg3. Jumps to Arg0 on error if it
is not zero.  Otherwise, raises an exception.


i_gc_bif3
------------------------------


<div class="args">i_gc_bif3 j I s I d</div>

Executes a guard BIF at the address Arg1 with three parameters &ndash; Arg2,
<b>tmpA</b>, and <b>tmpB</b>. Arg3 is Live. Stores the result in Arg4. Jumps to Arg0 on
error if it is not zero.  Otherwise, raises an exception.


i_get
------------------------------


<div class="args">i_get s d</div>

Reads the process dictionary key Arg0 and places the result to Arg1.


i_get_tuple_element
------------------------------


<div class="args">i_get_tuple_element rxy P rxy</div>

Gets the value of the the Arg1'th element of the tuple Arg0 and puts it to Arg2.
Arg1 is 1-based.


i_hibernate
------------------------------


<div class="args">i_hibernate</div>

Puts the process into a hibernated state dropping its stack and minimizing its
heap. When a message arrives or if the message queue is not empty the process is
waken up and starts executing a function identified by R0 (module), R1
(function), and R2 (arguments).


i_increment
------------------------------


<div class="args">i_increment rxy I I d</div>

Arg3 = Arg0 + Arg1. Arg2 is Live.


i_int_bnot
------------------------------


<div class="args">i_int_bnot j s I d</div>

Arg3 = ~ Arg1. Arg2 is Live. Jumps to Arg0 on error if Arg0 is not zero.


i_int_div
------------------------------


<div class="args">i_int_div j I d</div>

Arg2 = <b>tmpA</b> / <b>tmpB</b>. Division is integer. Arg1 is Live. Jumps to Arg0 on
error if Arg0 is not zero.


i_is_eq
------------------------------


<div class="args">i_is_eq f</div>

Checks if <b>tmpA</b> is equal to <b>tmpB</b>. Jumps to the label Arg0 if it is not.


i_is_eq_exact
------------------------------


<div class="args">i_is_eq_exact f</div>

Checks if <b>tmpA</b> 'exactly' equals <b>tmpB</b>. Jumps to the label Arg0 if it does
not.


i_is_eq_exact_immed
------------------------------


<div class="args">i_is_eq_exact_immed f rxy c</div>

Checks if Arg1 equals Arg2 using <em>bitwise</em> comparison. Jumps to Arg0 if it
does not.


i_is_eq_exact_literal
------------------------------


<div class="args">i_is_eq_exact_literal f rxy c</div>

Checks if Arg1 equals Arg2 using the term comparison. Jumps to Arg0 if it does not.


i_is_ge
------------------------------


<div class="args">i_is_ge f</div>

Checks if <b>tmpA</b> is greater than or equal to <b>tmpB</b>. Jumps to the label Arg0
if it is not.


i_is_lt
------------------------------


<div class="args">i_is_lt f</div>

Checks if <b>tmpA</b> is less than <b>tmpB</b>. Jumps to the label Arg0 if it is not.


i_is_ne
------------------------------


<div class="args">i_is_ne f</div>

Checks if <b>tmpA</b> is equal to <b>tmpB</b>. Jumps to the label Arg0 if it is.


i_is_ne_exact
------------------------------


<div class="args">i_is_ne_exact f</div>

Checks if <b>tmpA</b> 'exactly' equals <b>tmpB</b>. Jumps to the label Arg0 if it does.


i_is_ne_exact_immed
------------------------------


<div class="args">i_is_ne_exact_immed f rxy c</div>

Checks if Arg1 equals Arg2 using <em>bitwise</em> comparison. Jumps to Arg0 if it
does.


i_is_ne_exact_literal
------------------------------


<div class="args">i_is_ne_exact_literal f rxy c</div>

Checks if Arg1 equals Arg2 using the term comparison. Jumps to Arg0 if it does.


i_jump_on_val
------------------------------


<div class="args">i_jump_on_val rxy f I I</div>

Implements a 'jump table'. Calculates the index by adding Arg0 to the minimum
value Arg2. Jumps to Arg1 if the index falls outside of the table boundaries.
Arg3 is the length of the jump table. Picks the label from the table using the
calculated index and jumps there. 


i_jump_on_val_zero
------------------------------


<div class="args">i_jump_on_val_zero rxy f I</div>

Same as <span class="see" data-id="i_jump_on_val">i_jump_on_val rxy f I I</span> but the minimum value is assumed to be
zero.


i_loop_rec
------------------------------


<div class="args">i_loop_rec f r</div>

Picks the next message from the message queue and places it in R0. If there are
no messages then jumps to Arg0 which points to <span class="see" data-id="wait">wait</span>
or <span class="see" data-id="wait_timeout">wait_timeout</span> instruction.


i_make_fun
------------------------------


<div class="args">i_make_fun I t</div>

Creates a fun and puts it to R0. Arg0 contains a reference to the entry of the
lamdba table of the module. Arg1 is the number of free variables. The values of
free variables are taken from registers starting with R0. Only these registers
are considered live. It means that Arg1 is Live also.


i_m_div
------------------------------


<div class="args">i_m_div j I d</div>

Arg2 = <b>tmpA</b> / <b>tmpB</b>. Mixed. Arg1 is Live. Jumps to Arg0 on error if Arg0 is
not zero.


i_minus
------------------------------


<div class="args">i_minus j I d</div>

Arg2 = <b>tmpA</b> - <b>tmpB</b>. Arg1 is Live. Jumps to Arg0 on error if Arg0 is not
zero.


i_move_call
------------------------------


<div class="args">i_move_call c r f</div>

Combines <span class="see" data-id="move">move c r</span> and
<span class="see" data-id="call">call f</span>.


i_move_call_ext
------------------------------


<div class="args">i_move_call_ext c r e</div>

Combines <span class="see" data-id="move">move c r</span> with 
<span class="see" data-id="i_call_ext">i_call_ext e</span>.


i_move_call_ext_last
------------------------------


<div class="args">i_move_call_ext_last e P c r</div>

Combines <span class="see" data-id="move">move c r</span> with
<span class="see" data-id="i_call_last">i_call_last e</span>.


i_move_call_ext_only
------------------------------


<div class="args">i_move_call_ext_only e c r</div>

Combines <span class="see" data-id="move">move c r</span> with
<span class="see" data-id="i_call_only">i_call_only e</span>.


i_move_call_last
------------------------------


<div class="args">i_move_call_last f P c r</div>

Combines <span class="see" data-id="move">move c r</span> and
<span class="see" data-id="call_last">call_last f P</span>.


i_move_call_only
------------------------------


<div class="args">i_move_call_only f c r</div>

Combines <span class="see" data-id="move">move c r</span> and
<span class="see" data-id="call_only">call_only f</span>.


i_new_bs_put_binary
------------------------------


<div class="args">i_new_bs_put_binary j s I s</div>

Assumes that previous instructions created a binary creation context. Packs a
binary Arg3 of Arg1 units size into the context. Arg2 are flags and the unit.
The failure label Arg0 is not used.


i_new_bs_put_binary_all
------------------------------


<div class="args">i_new_bs_put_binary_all j s I</div>

Assumes that previous instructions created a binary creation context. Packs a
whole binary Arg1 into the context. Arg2 is the unit. The failure label Arg0 is
not used.


i_new_bs_put_binary_imm
------------------------------


<div class="args">i_new_bs_put_binary_imm j I s</div>

Assumes that previous instructions created a binary creation context. Packs a
binary Arg2 of Arg1 bits size into the context. The failure label Arg0 is not
used.


i_new_bs_put_float
------------------------------


<div class="args">i_new_bs_put_float j s I s</div>

Assumes that previous instructions created a binary creation context. Packs a
float of Arg1 units size into the context. Arg2 are the unit and flags. The
failure label Arg0 is not used.


i_new_bs_put_float_imm
------------------------------


<div class="args">i_new_bs_put_float_imm j I I s</div>

Assumes that previous instructions created a binary creation context. Packs a
float Arg3 of Arg1 bits size into the context. Arg2 are flags. The failure label Arg0
is not used.


i_new_bs_put_integer
------------------------------


<div class="args">i_new_bs_put_integer j s I s</div>

Assumes that previous instructions created a binary creation context. Packs an
integer value Arg3 into Arg1 units of the context. Arg2 are the unit and flags.
The failure label Arg0 is unused.


i_new_bs_put_integer_imm
------------------------------


<div class="args">i_new_bs_put_integer_imm j I I s</div>

Assumes that previous instructions created a binary creation context. Packs an
integer value Arg3 into Arg1 bits of the context. Arg2 are flags.  The failure
label Arg0 is unused.


init
------------------------------


<div class="args">init y</div>

Sets the Arg0 slot to nil. The op was called 'kill' earlier.


init2
------------------------------


<div class="args">init2 y y</div>

Sets slots Arg0 and Arg1 to nil.


init3
------------------------------


<div class="args">init3 y y y</div>

Sets slots Arg0, Arg1, and Arg2 to nil.


int_code_end
------------------------------


<div class="meta">Meta</div>

<div class="args">int_code_end</div>

Maybe marks the end of the code.


i_plus
------------------------------


<div class="args">i_plus j I d</div>

Arg2 = <b>tmpA</b> + <b>tmpB</b>. Arg1 is Live. Jumps to Arg0 on error if Arg0 is not
zero.


i_put_tuple
------------------------------


<div class="args">i_put_tuple rxy I</div>

Creates a tuple on the heap and places it in Arg0. Arg1 is the arity of the
tuple. The elements of the tuple follow the instruction. Some of the elements
may refer to registers or stack slots.


i_recv_set
------------------------------


<div class="args">i_recv_set f</div>

Sets the <b>SAVE</b> pointer to the saved last pointer if the label is right. This
is somehow needed for in-order processing of monitoring messages.


i_rem
------------------------------


<div class="args">i_rem j I d</div>

Arg2 = <b>tmpA</b> % <b>tmpB</b>. Division is integer. Arg1 is Live. Jumps to Arg0 on
error if Arg0 is not zero.


is_atom
------------------------------


<div class="args">is_atom f rxy</div>

Jumps to the label Arg0 if Arg1 is not an atom.


is_bitstring
------------------------------


<div class="args">is_bitstring f rxy</div>

Jumps to the label Arg0 if Arg1 is not a bitstring (or a binary).


is_boolean
------------------------------


<div class="args">is_boolean f rxy</div>

Jumps to the label Arg0 if Arg1 is not true or false.


i_select_tuple_arity
------------------------------


<div class="args">
i_select_tuple_arity r f I<br>
i_select_tuple_arity x f I<br>
i_select_tuple_arity y f I
</div>

Checks that Arg0 is tuple and then searches the array for {arity,addr} for the
right arity. See <span class="see" data-id="i_select_val">i_select_val rxy f I</span>.


i_select_tuple_arity2
------------------------------


<div class="args">
i_select_tuple_arity2 r f A f A f<br>
i_select_tuple_arity2 x f A f A f<br>
i_select_tuple_arity2 y f A f A f
</div>

Same as <span class="see" data-id="i_select_tuple_arity">i_select_tuple_arity rxy f I</span>
 but uses the array made up of two pairs: {Arg2,Arg3} and {Arg4,Arg5}.


i_select_val
------------------------------


<div class="args">
i_select_val r f I<br>
i_select_val x f I<br>
i_select_val y f I
</div>

Searches an array of {val,addr} pairs for the value of Arg0. The length
of the array is Arg2. If the value is found the execution continues at the
corresponding <em>addr</em>. Otherwise, jumps to Arg1. Uses binary search and
<em>bitwise</em> comparisons.


i_select_val2
------------------------------


<div class="args">
i_select_val2 r f c f c f<br>
i_select_val2 x f c f c f<br>
i_select_val2 y f c f c f
</div>

Same as <span class="see" data-id="i_select_val">i_select_val rxy f I</span> but uses an array made of
{Arg2,Arg3} and {Arg4,Arg5}.


is_float
------------------------------


<div class="args">is_float f rxy</div>

Jumps to the label Arg0 if Arg1 is not a float.


is_function
------------------------------


<div class="args">is_function f rxy</div>

Jumps to the label Arg0 if Arg1 is not a fun.


is_function2
------------------------------


<div class="args">is_function2 f s s</div>

Jumps to the label Arg0 if Arg1 is not fun or have an arity different from Arg1.


is_integer
------------------------------


<div class="args">is_integer f rxy</div>

Jumps to the label Arg0 if Arg1 is not integer.


is_integer_allocate
------------------------------


<div class="args">is_integer_allocate f rx I I</div>

Combines <span class="see" data-id="is_integer">is_integer f rx</span> and
<span class="see" data-id="allocate">allocate I I</span>.


is_list
------------------------------


<div class="args">is_list f rxy</div>

Jumps to the label Arg0 if Arg1 is not a list.


is_nil
------------------------------


<div class="args">is_nil f rxy</div>

Jumps to the label Arg0 if Arg1 is not nil.


is_nonempty_list
------------------------------


<div class="args">is_nonempty_list f rxy</div>

Jumps to the label Arg0 if Arg1 is not an nonempty list.


is_nonempty_list_allocate
------------------------------


<div class="args">is_nonempty_list_allocate f rx I t</div>

Combines <span class="see" data-id="is_nonempty_list">is_nonempty_list f rx</span>
 and <span class="see" data-id="allocate">allocate I t</span>.


is_nonempty_list_test_heap
------------------------------


<div class="args">is_nonempty_list_test_heap f r I t</div>

Combines <span class="see" data-id="is_nonempty_list">is_nonempty_list f r</span>
 and <span class="see" data-id="test_heap">test_heap I t</span>.


is_number
------------------------------


<div class="args">is_number f rxy</div>

Jumps to Arg0 if Arg1 is not integer and is not float.


is_pid
------------------------------


<div class="args">is_pid f rxy</div>

Jumps to the label Arg0 if Arg1 is not a pid.


is_port
------------------------------


<div class="args">is_port f rxy</div>

Jumps to the label Arg0 if Arg1 is not a port.


is_reference
------------------------------


<div class="args">is_reference f rxy</div>

Jumps to the label Arg0 if Arg1 is not a reference.


is_tuple
------------------------------


<div class="args">is_tuple f rxy</div>

Jumps to the label Arg0 if Arg1 is not a tuple.


is_tuple_of_arity
------------------------------


<div class="args">is_tuple_of_arity f rxy A</div>

Jumps to the label Arg0 if Arg1 is not a tuple or its arity is not Arg2. If Arg1
is tuple its value is saved to <b>tmpA</b>.


i_times
------------------------------


<div class="args">i_times j I d</div>

Arg2 = <b>tmpA</b> * <b>tmpB</b>. Mixed. Arg1 is Live. Jumps to Arg0 on error if Arg0 is
not zero.


i_trim
------------------------------


<div class="args">i_trim I</div>

Removes Arg0 slots from the stack. The saved <b>CP</b> is moved to the new top of the
stack.


i_wait_error
------------------------------


<div class="args">i_wait_error</div>

Raises a timeout_value exception.


i_wait_error_locked
------------------------------


<div class="args">i_wait_error_locked</div>

Same as <span class="see" data-id="i_wait_error">i_wait_error</span> but with due respect to SMP.


i_wait_timeout
------------------------------


<div class="args">
i_wait_timeout f I<br>
i_wait_timeout f s
</div>

Sets the timer to the appropriate time as indicated by Arg1. Afterwards acts as
<span class="see" data-id="wait">wait f</span>.


i_wait_timeout_locked
------------------------------


<div class="args">
i_wait_timeout_locked f I<br>
i_wait_timeout_locked f s
</div>

Same as <span class="see" data-id="i_wait_timeout">i_wait_timeout f I</span> but with SMP trickery.


jump
------------------------------


<div class="args">jump f</div>

Continues execution at the location Arg0.


label
------------------------------


<div class="meta">Meta</div>

<div class="args">label L</div>

The label L is set to the current code location.


line
------------------------------


<div class="meta">Meta</div>

<div class="args">line I</div>

Maybe augments debugging output when backtracking.


loop_rec_end
------------------------------


<div class="args">loop_rec_end f</div>

Advances the <b>SAVE</b> pointer to the next message as the current message did not
match. Jumps to Arg0 that points to <span class="see" data-id="loop_rec">loop_rec f r</span> instruction.


move
------------------------------


<div class="args">move rxync rxy</div>

Copies Arg0 to Arg1.


move2
------------------------------


<div class="args">
move2 x y x y<br>
move2 y x y x<br>
move2 x x x x
</div>

Combine two move operations.


move_call
------------------------------


<div class="args">move_call xy r f</div>

Same as <span class="see" data-id="i_move_call">i_move_call xy r f</span>.


move_call_last
------------------------------


<div class="args">move_call_last xy r f Q</div>

Same as <span class="see" data-id="i_move_last">i_move_last f Q xy r</span>.


move_call_only
------------------------------


<div class="args">move_call_only x r f</div>

Same as <span class="see" data-id="i_move_only">i_move_only xy r f</span>.


move_deallocate_return
------------------------------


<div class="args">move_deallocate_return xycn r Q</div>

Combines <span class="see" data-id="move">move xycn r</span>,
<span class="see" data-id="deallocate">deallocate Q</span>, and
<span class="see" data-id="return">return</span>.


move_jump
------------------------------


<div class="args">move_jump f ncxy</div>

Move the value from Arg1 to R0 and then jumps to the label Arg0.


move_return
------------------------------


<div class="args">move_return xcn r</div>

Combines <span class="see" data-id="move">move xcn r</span> and
<span class="see" data-id="return">return</span>.


move_x1
------------------------------


<div class="args">move_x1 c</div>

Sets R1 to the value of Arg0.


move_x2
------------------------------


<div class="args">move_x2 c</div>

Sets R2 to the value of Arg0.


node
------------------------------


<div class="args">node rxy</div>

Put the node identifier of the virtual machine to Arg0.


put_list
------------------------------


<div class="args">put_list s s d</div>

Create a cons cell on the heap and places in onto Arg2. Arg0 is the head of the
list saved to <b>HTOP</b>[0] and Arg1 is the tail saved to <b>HTOP</b>[1].


raise
------------------------------


<div class="args">raise s s</div>

Raises the exception. The instruction is garbled by backward compatibility. Arg0
is a stack trace and Arg1 is the value accompanying the exception. The reason of
the raised exception is dug up from the stack trace. 


recv_mark
------------------------------


<div class="args">recv_mark f</div>

Saves the last pointer of the message queue and the label of the soon expected
<span class="see" data-id="loop_rec">loop_rec f r</span>.


remove_message
------------------------------


<div class="args">remove_message</div>

Removes the (matched) message from the message queue.


return
------------------------------


<div class="args">return</div>

<b>IP</b> is set to <b>CP</b>.


self
------------------------------


<div class="args">self rxy</div>

Put the identifier of the current process to Arg0.


send
------------------------------


<div class="args">send</div>

Sends the message from R1 to the process R0.


set_tuple_element
------------------------------


<div class="args">set_tuple_element s d P</div>

Sets the Arg2'th element of the tuple Arg1 to to the value of Arg0. The index in
Arg2 is 1-based.


system_limit
------------------------------


<div class="args">system_limit j</div>

Similar to <span class="see" data-id="badarg">badarg j</span> but raises system_limit eption.


test_arity
------------------------------


<div class="args">test_arity f rxy A</div>

Jumps to the label Arg0 is the arity of the tuple Arg1 is not Arg2. The value of
Arg1 is saved to <b>tmpA</b>.


test_heap
------------------------------


<div class="args">test_heap I t</div>

Ensures that the heap has at least Arg0 words available. Arg1 is Live.


test_heap_1_put_list
------------------------------


<div class="args">test_heap_1_put_list I y</div>

Test that the heap has a room for Arg0 words and than conses value of Arg1 with
R0.


timeout
------------------------------


<div class="args">timeout</div>

Timeout has occured. Resets the <b>SAVE</b> pointer to the first message in the
message queue.


timeout_locked
------------------------------


<div class="args">timeout_locked</div>

Same as <span class="see" data-id="timeout">timeout</span> but with SMP precautions.


try_case_end
------------------------------


<div class="args">try_case_end s</div>

Raises a try_clause exception with the value read from Arg0.


try_end
------------------------------


<div class="args">try_end y</div>

Pops a 'catch' context. Erases the label saved in the Arg0 slot. Noval in R0
indicate that something is caught. If so, R0 is set to R1, R1 &ndash; to R2, R2 &ndash;
to R3.


wait
------------------------------


<div class="args">wait f</div>

Prepares to wait indefinitely for a message to arrive. When the message arrives
transfers control to the <span class="see" data-id="loop_rec">loop_rec</span> instruction at the label Arg0.


wait_locked
------------------------------


<div class="args">wait_locked f</div>

Same as <span class="see" data-id="wait">wait f</span>.


wait_unlocked
------------------------------


<div class="args">wait_unlocked f</div>

Same as <span class="see" data-id="wait">wait f</span> but messes with SMP locks.


