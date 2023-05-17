# Floating Point Numbers
C Guarantees Two Levels
• float single precision
• double double precision
• Conversions/Casting
• Casting between int, float, and double changes bit representation
• double/float → int
• Truncates fractional part
• Like rounding toward zero
• Not defined when out of range or NaN: Generally sets to TMin
• int → double
• Exact conversion, as long as int has ≤ 53 bit word size
• int → float
• Will round according to rounding mode
• Systems don’t usually use floats! :whew:
• Floats also suffer from the fixed number of bits available to represent
them
• Can get overflow/underflow
• “Gaps” produced in representable numbers means we can lose precision, unlike
ints
• Some “simple fractions” have no exact representation (e.g. 0.2)
• “Every operation gets a slightly wrong result”
• Floating point arithmetic not associative or distributive
• Mathematically equivalent ways of writing an expression may compute different
results
• Never test floating point values for exact equality!
• Careful when converting between ints and floats