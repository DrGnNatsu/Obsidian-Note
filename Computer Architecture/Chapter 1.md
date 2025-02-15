___
# Response Time and Throughput
| Throughput                     | Response Time                 |
| :----------------------------- | ----------------------------- |
| How long it takes to do a task | Total work done per unit time |
How are response time and throughput affected by 
- Replacing the processor with a faster version? 
- Adding more processors?
___
# Relative program
- Higher performance is better
- A shorter execution time is better
⇒ $Performance = \frac{1} {Execution\;Time}$
___
# Measuring time
| Elapsed time                                                                                                               | CPU Time                                                                                                                                                                                                         |
| :------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Total response time, including all aspects <br>• Processing, I/O, OS overhead, idle time <br>Determines system performance | Time spent processing a given job <br>• Discounts I/O time and other jobs’ shares <br>Comprises user CPU time and system CPU time <br>Different programs are affected differently by CPUs and system performance |
## Measuring CPU Time
![[CPU Time.png]]
- A constant-rate clock governs the operations of digital hardware (including CPU/processor).
- Clock Period  = Clock Cycle ($T$) Duration of a clock cycle (s)
- Clock rate = Frequency ($F = 1/T$): The number of cycles per second. (Hz)

$$CPU\;Time = CPU\;Clock\;Cycles \times Clock\;Cycle\;Time = \frac{CPU\;Clock\;Cycles}{Clock\;Rate}$$
Performance improved by: 
- Reducing number of clock cycles 
- Increasing clock rate 
- Hardware designers must often trade off clock rate against cycle count

### Improve CPU Time
- If we increase the `clock rate` two times, we do not get two times the performance because of side effects.
This happened because although we reduce the clock Cycle, the time for the logic gates to decide does not change, so if we reduce the clock cycle = we increase the number of times we make the decision. Therefore, it takes more time.
___
# Instruction Count & CPI
Instruction Count for a program: Determined by program, ISA and compiler (ISA is the set of instruction architecture like multiply or division)
Average cycles per instruction (CPI): 
- Determined by CPU hardware 
- If different instructions have different CPIs 
- Average CPI affected by instruction mix
$$CPU\;Clock\;Cycles = Instruction\;Count * CPI$$
$$CPU\;Time = Instruction\;Count \times CPI \times Clock\;Cycle\;Time = \frac {Instruction\;Count \times CPI} {Clock\;Rate}$$
## Mixed instructions CPI
$$Clock\;Cycles = \sum_{i=1}^{n} CPI_i * Instruction\;Count_i $$