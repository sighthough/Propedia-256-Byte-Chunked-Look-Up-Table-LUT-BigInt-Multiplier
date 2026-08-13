
# Propedia-256-Byte-Chunked-Look-Up-Table-LUT-BigInt-Multiplier

Propedia 256 is an arbitrary-precision multiplication engine designed to accelerate software-emulated BigInt math. By shifting processing from bit-by-bit loops to Base-256 (byte-wise) matrix multiplication, it reduces loop iterations by 87.5% while keeping memory consumption bounded at a fixed 128 KB.


demo showcasing its speed  [here](https://sighthough.github.io/Propedia-256-Byte-Chunked-Look-Up-Table-LUT-BigInt-Multiplier/)
compared to other methods all done in software for fair measurments




1. The Core ArchitectureTraditional software multiplication usually falls into one of two extremes:Bit-by-bit shift-and-add: Low memory, but extremely slow ($1024$ loop passes for $1024$-bit numbers).Full word Look-Up Tables: Unrealistic memory consumption ($65,536 \times 65,536$ entries for 16-bit chunks requires 8.5 GB of RAM).Propedia 256 solves this by decomposing arbitrarily large integers into 8-bit byte chunks ($0 \le c \le 255$) and computing partial products using a precomputed $256 \times 256$ Lookup Table.Input Number A (e.g. 256-bit)  --> [ A0 ][ A1 ][ A2 ] ... [ A31 ]  (32 Bytes)

   

Input Number B (e.g. 256-bit)  --> [ B0 ][ B1 ][ B2 ] ... [ B31 ]  (32 Bytes)

                                         |      |
                                         
                                         v      v
                                         
                                +-----------------------
                                |  128 KB Propedia LUT  |
                                | (256x256 Precomputed) |
                                +-----------------------+
                                
                                           |
                                           v
                                           
                             [ Uint32 Accumulation Grid ]

                                           |
                                           v
                             
                               [ Ripple-Carry Resolution ]
                               
                                           |
                                           v
                                   
                                   Result (512-bit)


for more info check the chat session i had with the ai that helped me make this a reality : https://share.gemini.google/lHMQMrySfViT

2026 [sighthough](https://youtu.be/UtPiUGwu-0Q)-gemini ai 3.6 thinking

