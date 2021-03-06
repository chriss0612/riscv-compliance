
# Data Propagation Report

- **STAT1** : Number of instructions that hit unique coverpoints and update the signature.
- **STAT2** : Number of instructions that hit covepoints which are not unique but still update the signature
- **STAT3** : Number of instructions that hit a unique coverpoint but do not update signature
- **STAT4** : Number of multiple signature updates for the same coverpoint
- **STAT5** : Number of times the signature was overwritten

| Param                     | Value    |
|---------------------------|----------|
| XLEN                      | 64      |
| TEST_REGION               | [('0x80000390', '0x800010a0')]      |
| SIG_REGION                | [('0x80003010', '0x800034e0', '154 dwords')]      |
| COV_LABELS                | sllw      |
| TEST_NAME                 | /scratch/git-repo/incoresemi/riscof/riscof_work/sllw-01.S/sllw-01.S    |
| Total Number of coverpoints| 275     |
| Total Coverpoints Hit     | 275      |
| Total Signature Updates   | 153      |
| STAT1                     | 150      |
| STAT2                     | 3      |
| STAT3                     | 0     |
| STAT4                     | 0     |
| STAT5                     | 0     |

## Details for STAT2:

```
Op without unique coverpoint updates Signature
 -- Code Sequence:
      [0x80001058]:sllw a2, a0, a1
      [0x8000105c]:sd a2, 1064(t0)
 -- Signature Address: 0x800034b8 Data: 0xFFFFFFFFFFFF8000
 -- Redundant Coverpoints hit by the op
      - opcode : sllw
      - rs1 : x10
      - rs2 : x11
      - rd : x12
      - rs1 != rs2  and rs1 != rd and rs2 != rd
      - rs1_val < 0 and rs2_val > 0 and rs2_val < xlen
      - rs1_val == -140737488355329
      - rs2_val == 15




Op without unique coverpoint updates Signature
 -- Code Sequence:
      [0x80001070]:sllw a2, a0, a1
      [0x80001074]:sd a2, 1072(t0)
 -- Signature Address: 0x800034c0 Data: 0xFFFFFFFFFF800000
 -- Redundant Coverpoints hit by the op
      - opcode : sllw
      - rs1 : x10
      - rs2 : x11
      - rd : x12
      - rs1 != rs2  and rs1 != rd and rs2 != rd
      - rs1_val > 0 and rs2_val > 0 and rs2_val < xlen
      - rs1_val == (2**(xlen-1)-1) and rs2_val >= 0 and rs2_val < xlen
      - rs1_val == 9223372036854775807
      - rs2_val == 23




Op without unique coverpoint updates Signature
 -- Code Sequence:
      [0x80001080]:sllw a2, a0, a1
      [0x80001084]:sd a2, 1080(t0)
 -- Signature Address: 0x800034c8 Data: 0x0000000000800000
 -- Redundant Coverpoints hit by the op
      - opcode : sllw
      - rs1 : x10
      - rs2 : x11
      - rd : x12
      - rs1 != rs2  and rs1 != rd and rs2 != rd
      - rs1_val > 0 and rs2_val > 0 and rs2_val < xlen
      - rs1_val == 64






```

## Details of STAT3

```


```

## Details of STAT4:

```

```

## Details of STAT5:



## Details of STAT1:

- The first column indicates the signature address and the data at that location in hexadecimal in the following format: 
  ```
  [Address]
  Data
  ```

- The second column captures all the coverpoints which have been captured by that particular signature location

- The third column captures all the insrtuctions since the time a coverpoint was
  hit to the point when a store to the signature was performed. Each line has
  the following format:
  ```
  [PC of instruction] : mnemonic
  ```
- The order in the table is based on the order of signatures occuring in the
  test. These need not necessarily be in increasing or decreasing order of the
  address in the signature region.

|s.no|            signature             |                                                                                                           coverpoints                                                                                                           |                                code                                 |
|---:|----------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------|
|   1|[0x80003010]<br>0xFFFFFFFF80000000|- opcode : sllw<br> - rs1 : x7<br> - rs2 : x7<br> - rd : x14<br> - rs1 == rs2 != rd<br> - rs1_val == -140737488355329<br>                                                                                                        |[0x800003b0]:sllw a4, t2, t2<br> [0x800003b4]:sd a4, 0(tp)<br>       |
|   2|[0x80003018]<br>0x0000000000000000|- rs1 : x27<br> - rs2 : x30<br> - rd : x30<br> - rs2 == rd != rs1<br> - rs1_val > 0 and rs2_val > 0 and rs2_val < xlen<br> - rs1_val == 288230376151711744<br> - rs2_val == 23<br>                                               |[0x800003c4]:sllw t5, s11, t5<br> [0x800003c8]:sd t5, 8(tp)<br>      |
|   3|[0x80003020]<br>0xFFFFFFFFE8000000|- rs1 : x5<br> - rs2 : x5<br> - rd : x5<br> - rs1 == rs2 == rd<br>                                                                                                                                                               |[0x800003d4]:sllw t0, t0, t0<br> [0x800003d8]:sd t0, 16(tp)<br>      |
|   4|[0x80003028]<br>0x0000000010000000|- rs1 : x18<br> - rs2 : x15<br> - rd : x22<br> - rs1 != rs2  and rs1 != rd and rs2 != rd<br> - rs1_val > 0 and rs2_val == 0<br> - rs1_val == 268435456<br>                                                                       |[0x800003e4]:sllw s6, s2, a5<br> [0x800003e8]:sd s6, 24(tp)<br>      |
|   5|[0x80003030]<br>0x00000000000000A0|- rs1 : x26<br> - rs2 : x22<br> - rd : x26<br> - rs1 == rd != rs2<br> - rs1_val == rs2_val and rs2_val > 0 and rs2_val < xlen<br> - rs1_val==5<br>                                                                               |[0x800003f4]:sllw s10, s10, s6<br> [0x800003f8]:sd s10, 32(tp)<br>   |
|   6|[0x80003038]<br>0x0000000000000000|- rs1 : x14<br> - rs2 : x23<br> - rd : x29<br> - rs1_val < 0 and rs2_val > 0 and rs2_val < xlen<br> - rs1_val == (-2**(xlen-1)) and rs2_val >= 0 and rs2_val < xlen<br> - rs1_val == -9223372036854775808<br> - rs2_val == 2<br> |[0x80000408]:sllw t4, a4, s7<br> [0x8000040c]:sd t4, 40(tp)<br>      |
|   7|[0x80003040]<br>0x0000000000000000|- rs1 : x12<br> - rs2 : x14<br> - rd : x9<br> - rs1_val == 0 and rs2_val >= 0 and rs2_val < xlen<br> - rs1_val==0<br>                                                                                                            |[0x80000418]:sllw s1, a2, a4<br> [0x8000041c]:sd s1, 48(tp)<br>      |
|   8|[0x80003048]<br>0xFFFFFFFFFFFFFFFF|- rs1 : x10<br> - rs2 : x0<br> - rd : x1<br> - rs1_val == (2**(xlen-1)-1) and rs2_val >= 0 and rs2_val < xlen<br> - rs1_val == 9223372036854775807<br>                                                                           |[0x80000430]:sllw ra, a0, zero<br> [0x80000434]:sd ra, 56(tp)<br>    |
|   9|[0x80003050]<br>0x0000000000200000|- rs1 : x31<br> - rs2 : x8<br> - rd : x19<br> - rs1_val == 1 and rs2_val >= 0 and rs2_val < xlen<br> - rs1_val == 1<br> - rs2_val == 21<br>                                                                                      |[0x80000440]:sllw s3, t6, fp<br> [0x80000444]:sd s3, 64(tp)<br>      |
|  10|[0x80003058]<br>0x0000000001000000|- rs1 : x23<br> - rs2 : x27<br> - rd : x17<br> - rs1_val == 2<br> - rs1_val==2<br>                                                                                                                                               |[0x80000450]:sllw a7, s7, s11<br> [0x80000454]:sd a7, 72(tp)<br>     |
|  11|[0x80003060]<br>0x0000000000000400|- rs1 : x17<br> - rs2 : x26<br> - rd : x25<br> - rs1_val == 4<br> - rs1_val==4<br> - rs2_val == 8<br>                                                                                                                            |[0x80000460]:sllw s9, a7, s10<br> [0x80000464]:sd s9, 80(tp)<br>     |
|  12|[0x80003068]<br>0x0000000000000008|- rs1 : x11<br> - rs2 : x12<br> - rd : x16<br> - rs1_val == 8<br>                                                                                                                                                                |[0x80000470]:sllw a6, a1, a2<br> [0x80000474]:sd a6, 88(tp)<br>      |
|  13|[0x80003070]<br>0x0000000000000010|- rs1 : x24<br> - rs2 : x3<br> - rd : x27<br> - rs1_val == 16<br>                                                                                                                                                                |[0x80000480]:sllw s11, s8, gp<br> [0x80000484]:sd s11, 96(tp)<br>    |
|  14|[0x80003078]<br>0x0000000000000080|- rs1 : x16<br> - rs2 : x10<br> - rd : x7<br> - rs1_val == 32<br>                                                                                                                                                                |[0x80000490]:sllw t2, a6, a0<br> [0x80000494]:sd t2, 104(tp)<br>     |
|  15|[0x80003080]<br>0x0000000000000000|- rs1 : x2<br> - rs2 : x1<br> - rd : x0<br> - rs1_val == 64<br>                                                                                                                                                                  |[0x800004a0]:sllw zero, sp, ra<br> [0x800004a4]:sd zero, 112(tp)<br> |
|  16|[0x80003088]<br>0x0000000000000080|- rs1 : x28<br> - rs2 : x21<br> - rd : x6<br> - rs1_val == 128<br>                                                                                                                                                               |[0x800004b0]:sllw t1, t3, s5<br> [0x800004b4]:sd t1, 120(tp)<br>     |
|  17|[0x80003090]<br>0x0000000000004000|- rs1 : x8<br> - rs2 : x17<br> - rd : x13<br> - rs1_val == 256<br>                                                                                                                                                               |[0x800004c8]:sllw a3, fp, a7<br> [0x800004cc]:sd a3, 0(t0)<br>       |
|  18|[0x80003098]<br>0x0000000000001000|- rs1 : x21<br> - rs2 : x13<br> - rd : x20<br> - rs1_val == 512<br>                                                                                                                                                              |[0x800004d8]:sllw s4, s5, a3<br> [0x800004dc]:sd s4, 8(t0)<br>       |
|  19|[0x800030a0]<br>0x0000000000040000|- rs1 : x25<br> - rs2 : x28<br> - rd : x18<br> - rs1_val == 1024<br>                                                                                                                                                             |[0x800004e8]:sllw s2, s9, t3<br> [0x800004ec]:sd s2, 16(t0)<br>      |
|  20|[0x800030a8]<br>0x0000000000001000|- rs1 : x15<br> - rs2 : x11<br> - rd : x2<br> - rs1_val == 2048<br> - rs2_val == 1<br>                                                                                                                                           |[0x800004fc]:sllw sp, a5, a1<br> [0x80000500]:sd sp, 24(t0)<br>      |
|  21|[0x800030b0]<br>0x0000000000200000|- rs1 : x19<br> - rs2 : x9<br> - rd : x28<br> - rs1_val == 4096<br>                                                                                                                                                              |[0x8000050c]:sllw t3, s3, s1<br> [0x80000510]:sd t3, 32(t0)<br>      |
|  22|[0x800030b8]<br>0xFFFFFFFF80000000|- rs1 : x6<br> - rs2 : x20<br> - rd : x31<br> - rs1_val == 8192<br>                                                                                                                                                              |[0x8000051c]:sllw t6, t1, s4<br> [0x80000520]:sd t6, 40(t0)<br>      |
|  23|[0x800030c0]<br>0x0000000000400000|- rs1 : x1<br> - rs2 : x16<br> - rd : x3<br> - rs1_val == 16384<br>                                                                                                                                                              |[0x8000052c]:sllw gp, ra, a6<br> [0x80000530]:sd gp, 48(t0)<br>      |
|  24|[0x800030c8]<br>0x0000000010000000|- rs1 : x13<br> - rs2 : x29<br> - rd : x11<br> - rs1_val == 32768<br>                                                                                                                                                            |[0x8000053c]:sllw a1, a3, t4<br> [0x80000540]:sd a1, 56(t0)<br>      |
|  25|[0x800030d0]<br>0x0000000000010000|- rs1 : x22<br> - rs2 : x2<br> - rd : x10<br> - rs1_val == 65536<br>                                                                                                                                                             |[0x8000054c]:sllw a0, s6, sp<br> [0x80000550]:sd a0, 64(t0)<br>      |
|  26|[0x800030d8]<br>0x0000000008000000|- rs1 : x3<br> - rs2 : x19<br> - rd : x4<br> - rs1_val == 131072<br> - rs2_val == 10<br>                                                                                                                                         |[0x8000055c]:sllw tp, gp, s3<br> [0x80000560]:sd tp, 72(t0)<br>      |
|  27|[0x800030e0]<br>0x0000000000800000|- rs1 : x20<br> - rs2 : x6<br> - rd : x8<br> - rs1_val == 262144<br>                                                                                                                                                             |[0x8000056c]:sllw fp, s4, t1<br> [0x80000570]:sd fp, 80(t0)<br>      |
|  28|[0x800030e8]<br>0x0000000000000000|- rs1 : x9<br> - rs2 : x31<br> - rd : x12<br> - rs1_val == 524288<br> - rs2_val == 27<br>                                                                                                                                        |[0x8000057c]:sllw a2, s1, t6<br> [0x80000580]:sd a2, 88(t0)<br>      |
|  29|[0x800030f0]<br>0x0000000001000000|- rs1 : x30<br> - rs2 : x4<br> - rd : x24<br> - rs1_val == 1048576<br> - rs2_val == 4<br>                                                                                                                                        |[0x8000058c]:sllw s8, t5, tp<br> [0x80000590]:sd s8, 96(t0)<br>      |
|  30|[0x800030f8]<br>0x0000000020000000|- rs1 : x29<br> - rs2 : x25<br> - rd : x23<br> - rs1_val == 2097152<br>                                                                                                                                                          |[0x8000059c]:sllw s7, t4, s9<br> [0x800005a0]:sd s7, 104(t0)<br>     |
|  31|[0x80003100]<br>0x0000000000000000|- rs1 : x0<br> - rs2 : x24<br> - rd : x21<br>                                                                                                                                                                                    |[0x800005ac]:sllw s5, zero, s8<br> [0x800005b0]:sd s5, 112(t0)<br>   |
|  32|[0x80003108]<br>0x0000000000000000|- rs1 : x4<br> - rs2 : x18<br> - rd : x15<br> - rs1_val == 8388608<br>                                                                                                                                                           |[0x800005bc]:sllw a5, tp, s2<br> [0x800005c0]:sd a5, 120(t0)<br>     |
|  33|[0x80003110]<br>0x0000000000000000|- rs1_val == 16777216<br>                                                                                                                                                                                                        |[0x800005cc]:sllw a2, a0, a1<br> [0x800005d0]:sd a2, 128(t0)<br>     |
|  34|[0x80003118]<br>0x0000000000000000|- rs1_val == 33554432<br>                                                                                                                                                                                                        |[0x800005dc]:sllw a2, a0, a1<br> [0x800005e0]:sd a2, 136(t0)<br>     |
|  35|[0x80003120]<br>0x0000000000000000|- rs1_val == 67108864<br>                                                                                                                                                                                                        |[0x800005ec]:sllw a2, a0, a1<br> [0x800005f0]:sd a2, 144(t0)<br>     |
|  36|[0x80003128]<br>0x0000000000000000|- rs1_val == 134217728<br>                                                                                                                                                                                                       |[0x800005fc]:sllw a2, a0, a1<br> [0x80000600]:sd a2, 152(t0)<br>     |
|  37|[0x80003130]<br>0x0000000000000000|- rs1_val == 536870912<br> - rs2_val == 29<br>                                                                                                                                                                                   |[0x8000060c]:sllw a2, a0, a1<br> [0x80000610]:sd a2, 160(t0)<br>     |
|  38|[0x80003138]<br>0x0000000000000000|- rs1_val == 1073741824<br>                                                                                                                                                                                                      |[0x8000061c]:sllw a2, a0, a1<br> [0x80000620]:sd a2, 168(t0)<br>     |
|  39|[0x80003140]<br>0x0000000000000000|- rs1_val == 2147483648<br>                                                                                                                                                                                                      |[0x80000630]:sllw a2, a0, a1<br> [0x80000634]:sd a2, 176(t0)<br>     |
|  40|[0x80003148]<br>0x0000000000000000|- rs1_val == 4294967296<br>                                                                                                                                                                                                      |[0x80000644]:sllw a2, a0, a1<br> [0x80000648]:sd a2, 184(t0)<br>     |
|  41|[0x80003150]<br>0x0000000000000000|- rs1_val == 8589934592<br>                                                                                                                                                                                                      |[0x80000658]:sllw a2, a0, a1<br> [0x8000065c]:sd a2, 192(t0)<br>     |
|  42|[0x80003158]<br>0x0000000000000000|- rs1_val == 17179869184<br>                                                                                                                                                                                                     |[0x8000066c]:sllw a2, a0, a1<br> [0x80000670]:sd a2, 200(t0)<br>     |
|  43|[0x80003160]<br>0x0000000000000000|- rs1_val == 34359738368<br>                                                                                                                                                                                                     |[0x80000680]:sllw a2, a0, a1<br> [0x80000684]:sd a2, 208(t0)<br>     |
|  44|[0x80003168]<br>0x0000000000000000|- rs1_val == 68719476736<br>                                                                                                                                                                                                     |[0x80000694]:sllw a2, a0, a1<br> [0x80000698]:sd a2, 216(t0)<br>     |
|  45|[0x80003170]<br>0x0000000000000000|- rs1_val == 137438953472<br>                                                                                                                                                                                                    |[0x800006a8]:sllw a2, a0, a1<br> [0x800006ac]:sd a2, 224(t0)<br>     |
|  46|[0x80003178]<br>0x0000000000000000|- rs1_val == 274877906944<br>                                                                                                                                                                                                    |[0x800006bc]:sllw a2, a0, a1<br> [0x800006c0]:sd a2, 232(t0)<br>     |
|  47|[0x80003180]<br>0x0000000000000000|- rs1_val == 549755813888<br>                                                                                                                                                                                                    |[0x800006d0]:sllw a2, a0, a1<br> [0x800006d4]:sd a2, 240(t0)<br>     |
|  48|[0x80003188]<br>0x0000000000000000|- rs1_val == 1099511627776<br>                                                                                                                                                                                                   |[0x800006e4]:sllw a2, a0, a1<br> [0x800006e8]:sd a2, 248(t0)<br>     |
|  49|[0x80003190]<br>0x0000000000000000|- rs1_val == 2199023255552<br>                                                                                                                                                                                                   |[0x800006f8]:sllw a2, a0, a1<br> [0x800006fc]:sd a2, 256(t0)<br>     |
|  50|[0x80003198]<br>0x0000000000000000|- rs1_val == 4398046511104<br>                                                                                                                                                                                                   |[0x8000070c]:sllw a2, a0, a1<br> [0x80000710]:sd a2, 264(t0)<br>     |
|  51|[0x800031a0]<br>0x0000000000000000|- rs1_val == 8796093022208<br>                                                                                                                                                                                                   |[0x80000720]:sllw a2, a0, a1<br> [0x80000724]:sd a2, 272(t0)<br>     |
|  52|[0x800031a8]<br>0x0000000000000000|- rs1_val == 17592186044416<br>                                                                                                                                                                                                  |[0x80000734]:sllw a2, a0, a1<br> [0x80000738]:sd a2, 280(t0)<br>     |
|  53|[0x800031b0]<br>0x0000000000000000|- rs1_val == 35184372088832<br>                                                                                                                                                                                                  |[0x80000748]:sllw a2, a0, a1<br> [0x8000074c]:sd a2, 288(t0)<br>     |
|  54|[0x800031b8]<br>0x0000000000000000|- rs1_val == 70368744177664<br>                                                                                                                                                                                                  |[0x8000075c]:sllw a2, a0, a1<br> [0x80000760]:sd a2, 296(t0)<br>     |
|  55|[0x800031c0]<br>0x0000000000000000|- rs1_val == 140737488355328<br> - rs2_val == 30<br>                                                                                                                                                                             |[0x80000770]:sllw a2, a0, a1<br> [0x80000774]:sd a2, 304(t0)<br>     |
|  56|[0x800031c8]<br>0x0000000000000000|- rs1_val == 281474976710656<br>                                                                                                                                                                                                 |[0x80000784]:sllw a2, a0, a1<br> [0x80000788]:sd a2, 312(t0)<br>     |
|  57|[0x800031d0]<br>0x0000000000000000|- rs1_val == 562949953421312<br>                                                                                                                                                                                                 |[0x80000798]:sllw a2, a0, a1<br> [0x8000079c]:sd a2, 320(t0)<br>     |
|  58|[0x800031d8]<br>0x0000000000000000|- rs1_val == 1125899906842624<br>                                                                                                                                                                                                |[0x800007ac]:sllw a2, a0, a1<br> [0x800007b0]:sd a2, 328(t0)<br>     |
|  59|[0x800031e0]<br>0x0000000000000000|- rs1_val == 2251799813685248<br>                                                                                                                                                                                                |[0x800007c0]:sllw a2, a0, a1<br> [0x800007c4]:sd a2, 336(t0)<br>     |
|  60|[0x800031e8]<br>0x0000000000000000|- rs1_val == 4503599627370496<br> - rs2_val == 16<br>                                                                                                                                                                            |[0x800007d4]:sllw a2, a0, a1<br> [0x800007d8]:sd a2, 344(t0)<br>     |
|  61|[0x800031f0]<br>0x0000000000000000|- rs1_val == 9007199254740992<br>                                                                                                                                                                                                |[0x800007e8]:sllw a2, a0, a1<br> [0x800007ec]:sd a2, 352(t0)<br>     |
|  62|[0x800031f8]<br>0x0000000000000000|- rs1_val == 18014398509481984<br>                                                                                                                                                                                               |[0x800007fc]:sllw a2, a0, a1<br> [0x80000800]:sd a2, 360(t0)<br>     |
|  63|[0x80003200]<br>0x0000000000000000|- rs1_val == 36028797018963968<br>                                                                                                                                                                                               |[0x80000810]:sllw a2, a0, a1<br> [0x80000814]:sd a2, 368(t0)<br>     |
|  64|[0x80003208]<br>0x0000000000000000|- rs1_val == 72057594037927936<br>                                                                                                                                                                                               |[0x80000824]:sllw a2, a0, a1<br> [0x80000828]:sd a2, 376(t0)<br>     |
|  65|[0x80003210]<br>0x0000000000000000|- rs1_val == 144115188075855872<br>                                                                                                                                                                                              |[0x80000838]:sllw a2, a0, a1<br> [0x8000083c]:sd a2, 384(t0)<br>     |
|  66|[0x80003218]<br>0x0000000000000000|- rs1_val == 576460752303423488<br>                                                                                                                                                                                              |[0x8000084c]:sllw a2, a0, a1<br> [0x80000850]:sd a2, 392(t0)<br>     |
|  67|[0x80003220]<br>0x0000000000000000|- rs1_val == 1152921504606846976<br>                                                                                                                                                                                             |[0x80000860]:sllw a2, a0, a1<br> [0x80000864]:sd a2, 400(t0)<br>     |
|  68|[0x80003228]<br>0x0000000000000000|- rs1_val == 2305843009213693952<br>                                                                                                                                                                                             |[0x80000874]:sllw a2, a0, a1<br> [0x80000878]:sd a2, 408(t0)<br>     |
|  69|[0x80003230]<br>0x0000000000000000|- rs1_val == 4611686018427387904<br>                                                                                                                                                                                             |[0x80000888]:sllw a2, a0, a1<br> [0x8000088c]:sd a2, 416(t0)<br>     |
|  70|[0x80003238]<br>0xFFFFFFFFFFFFC000|- rs1_val == -2<br>                                                                                                                                                                                                              |[0x80000898]:sllw a2, a0, a1<br> [0x8000089c]:sd a2, 424(t0)<br>     |
|  71|[0x80003240]<br>0xFFFFFFFFFFFFA000|- rs1_val == -3<br>                                                                                                                                                                                                              |[0x800008a8]:sllw a2, a0, a1<br> [0x800008ac]:sd a2, 432(t0)<br>     |
|  72|[0x80003248]<br>0xFFFFFFFFFFFF6000|- rs1_val == -5<br>                                                                                                                                                                                                              |[0x800008b8]:sllw a2, a0, a1<br> [0x800008bc]:sd a2, 440(t0)<br>     |
|  73|[0x80003250]<br>0xFFFFFFFFFFFFFFB8|- rs1_val == -9<br>                                                                                                                                                                                                              |[0x800008c8]:sllw a2, a0, a1<br> [0x800008cc]:sd a2, 448(t0)<br>     |
|  74|[0x80003258]<br>0xFFFFFFFFFFFFFEF0|- rs1_val == -17<br>                                                                                                                                                                                                             |[0x800008d8]:sllw a2, a0, a1<br> [0x800008dc]:sd a2, 456(t0)<br>     |
|  75|[0x80003260]<br>0xFFFFFFFFFFFFEF80|- rs1_val == -33<br>                                                                                                                                                                                                             |[0x800008e8]:sllw a2, a0, a1<br> [0x800008ec]:sd a2, 464(t0)<br>     |
|  76|[0x80003268]<br>0xFFFFFFFFFFFFDF80|- rs1_val == -65<br>                                                                                                                                                                                                             |[0x800008f8]:sllw a2, a0, a1<br> [0x800008fc]:sd a2, 472(t0)<br>     |
|  77|[0x80003270]<br>0xFFFFFFFFFDFC0000|- rs1_val == -129<br>                                                                                                                                                                                                            |[0x80000908]:sllw a2, a0, a1<br> [0x8000090c]:sd a2, 480(t0)<br>     |
|  78|[0x80003278]<br>0xFFFFFFFFFFFEFF00|- rs1_val == -257<br>                                                                                                                                                                                                            |[0x80000918]:sllw a2, a0, a1<br> [0x8000091c]:sd a2, 488(t0)<br>     |
|  79|[0x80003280]<br>0xFFFFFFFFFFFF7FC0|- rs1_val == -513<br>                                                                                                                                                                                                            |[0x80000928]:sllw a2, a0, a1<br> [0x8000092c]:sd a2, 496(t0)<br>     |
|  80|[0x80003288]<br>0xFFFFFFFFFFFFEFFC|- rs1_val == -1025<br>                                                                                                                                                                                                           |[0x80000938]:sllw a2, a0, a1<br> [0x8000093c]:sd a2, 504(t0)<br>     |
|  81|[0x80003290]<br>0xFFFFFFFFC0000000|- rs1_val == -2049<br>                                                                                                                                                                                                           |[0x8000094c]:sllw a2, a0, a1<br> [0x80000950]:sd a2, 512(t0)<br>     |
|  82|[0x80003298]<br>0xFFFFFFFFFFFDFFE0|- rs1_val == -4097<br>                                                                                                                                                                                                           |[0x80000960]:sllw a2, a0, a1<br> [0x80000964]:sd a2, 520(t0)<br>     |
|  83|[0x800032a0]<br>0xFFFFFFFFFFFBFFE0|- rs1_val == -8193<br>                                                                                                                                                                                                           |[0x80000974]:sllw a2, a0, a1<br> [0x80000978]:sd a2, 528(t0)<br>     |
|  84|[0x800032a8]<br>0xFFFFFFFFFFDFFF80|- rs1_val == -16385<br>                                                                                                                                                                                                          |[0x80000988]:sllw a2, a0, a1<br> [0x8000098c]:sd a2, 536(t0)<br>     |
|  85|[0x800032b0]<br>0xFFFFFFFFFFF80000|- rs1_val == -32769<br>                                                                                                                                                                                                          |[0x8000099c]:sllw a2, a0, a1<br> [0x800009a0]:sd a2, 544(t0)<br>     |
|  86|[0x800032b8]<br>0xFFFFFFFFFFFE0000|- rs1_val == -65537<br>                                                                                                                                                                                                          |[0x800009b0]:sllw a2, a0, a1<br> [0x800009b4]:sd a2, 552(t0)<br>     |
|  87|[0x800032c0]<br>0xFFFFFFFFE0000000|- rs1_val == -131073<br>                                                                                                                                                                                                         |[0x800009c4]:sllw a2, a0, a1<br> [0x800009c8]:sd a2, 560(t0)<br>     |
|  88|[0x800032c8]<br>0xFFFFFFFFFBFFFF00|- rs1_val == -262145<br>                                                                                                                                                                                                         |[0x800009d8]:sllw a2, a0, a1<br> [0x800009dc]:sd a2, 568(t0)<br>     |
|  89|[0x800032d0]<br>0xFFFFFFFFFFFFFFC0|- rs1_val == -36028797018963969<br>                                                                                                                                                                                              |[0x800009f0]:sllw a2, a0, a1<br> [0x800009f4]:sd a2, 576(t0)<br>     |
|  90|[0x800032d8]<br>0xFFFFFFFFFF800000|- rs1_val == -72057594037927937<br>                                                                                                                                                                                              |[0x80000a08]:sllw a2, a0, a1<br> [0x80000a0c]:sd a2, 584(t0)<br>     |
|  91|[0x800032e0]<br>0xFFFFFFFFF8000000|- rs1_val == -144115188075855873<br>                                                                                                                                                                                             |[0x80000a20]:sllw a2, a0, a1<br> [0x80000a24]:sd a2, 592(t0)<br>     |
|  92|[0x800032e8]<br>0xFFFFFFFFFFFFFF80|- rs1_val == -288230376151711745<br>                                                                                                                                                                                             |[0x80000a38]:sllw a2, a0, a1<br> [0x80000a3c]:sd a2, 600(t0)<br>     |
|  93|[0x800032f0]<br>0xFFFFFFFFFFFFE000|- rs1_val == -576460752303423489<br>                                                                                                                                                                                             |[0x80000a50]:sllw a2, a0, a1<br> [0x80000a54]:sd a2, 608(t0)<br>     |
|  94|[0x800032f8]<br>0xFFFFFFFFE0000000|- rs1_val == -1152921504606846977<br>                                                                                                                                                                                            |[0x80000a68]:sllw a2, a0, a1<br> [0x80000a6c]:sd a2, 616(t0)<br>     |
|  95|[0x80003300]<br>0xFFFFFFFF80000000|- rs1_val == -2305843009213693953<br>                                                                                                                                                                                            |[0x80000a80]:sllw a2, a0, a1<br> [0x80000a84]:sd a2, 624(t0)<br>     |
|  96|[0x80003308]<br>0xFFFFFFFFFFF80000|- rs1_val == -4611686018427387905<br>                                                                                                                                                                                            |[0x80000a98]:sllw a2, a0, a1<br> [0x80000a9c]:sd a2, 632(t0)<br>     |
|  97|[0x80003310]<br>0x0000000055555554|- rs1_val == 6148914691236517205<br> - rs1_val==6148914691236517205<br>                                                                                                                                                          |[0x80000ac4]:sllw a2, a0, a1<br> [0x80000ac8]:sd a2, 640(t0)<br>     |
|  98|[0x80003318]<br>0x0000000055550000|- rs1_val == -6148914691236517206<br> - rs1_val==-6148914691236517206<br> - rs2_val == 15<br>                                                                                                                                    |[0x80000af0]:sllw a2, a0, a1<br> [0x80000af4]:sd a2, 648(t0)<br>     |
|  99|[0x80003320]<br>0x0000000001800000|- rs1_val==3<br>                                                                                                                                                                                                                 |[0x80000b00]:sllw a2, a0, a1<br> [0x80000b04]:sd a2, 656(t0)<br>     |
| 100|[0x80003328]<br>0xFFFFFFFF99980000|- rs1_val==3689348814741910323<br>                                                                                                                                                                                               |[0x80000b2c]:sllw a2, a0, a1<br> [0x80000b30]:sd a2, 664(t0)<br>     |
| 101|[0x80003330]<br>0xFFFFFFFFCCCC0000|- rs1_val==7378697629483820646<br>                                                                                                                                                                                               |[0x80000b58]:sllw a2, a0, a1<br> [0x80000b5c]:sd a2, 672(t0)<br>     |
| 102|[0x80003338]<br>0x0000000068000000|- rs1_val==-3037000499<br>                                                                                                                                                                                                       |[0x80000b74]:sllw a2, a0, a1<br> [0x80000b78]:sd a2, 680(t0)<br>     |
| 103|[0x80003340]<br>0x00000000504F3330|- rs1_val==3037000499<br>                                                                                                                                                                                                        |[0x80000b90]:sllw a2, a0, a1<br> [0x80000b94]:sd a2, 688(t0)<br>     |
| 104|[0x80003348]<br>0xFFFFFFFFAAAAAAA8|- rs1_val==6148914691236517204<br>                                                                                                                                                                                               |[0x80000bbc]:sllw a2, a0, a1<br> [0x80000bc0]:sd a2, 696(t0)<br>     |
| 105|[0x80003350]<br>0xFFFFFFFFCCCC8000|- rs1_val==3689348814741910322<br>                                                                                                                                                                                               |[0x80000be8]:sllw a2, a0, a1<br> [0x80000bec]:sd a2, 704(t0)<br>     |
| 106|[0x80003358]<br>0x0000000066666650|- rs1_val==7378697629483820645<br>                                                                                                                                                                                               |[0x80000c14]:sllw a2, a0, a1<br> [0x80000c18]:sd a2, 712(t0)<br>     |
| 107|[0x80003360]<br>0xFFFFFFFFE6640000|- rs1_val==3037000498<br>                                                                                                                                                                                                        |[0x80000c30]:sllw a2, a0, a1<br> [0x80000c34]:sd a2, 720(t0)<br>     |
| 108|[0x80003368]<br>0xFFFFFFFFAAAAAAAC|- rs1_val==6148914691236517206<br>                                                                                                                                                                                               |[0x80000c5c]:sllw a2, a0, a1<br> [0x80000c60]:sd a2, 728(t0)<br>     |
| 109|[0x80003370]<br>0xFFFFFFFFAAAB0000|- rs1_val==-6148914691236517205<br>                                                                                                                                                                                              |[0x80000c88]:sllw a2, a0, a1<br> [0x80000c8c]:sd a2, 736(t0)<br>     |
| 110|[0x80003378]<br>0x0000000000000000|- rs1_val==6<br>                                                                                                                                                                                                                 |[0x80000c98]:sllw a2, a0, a1<br> [0x80000c9c]:sd a2, 744(t0)<br>     |
| 111|[0x80003380]<br>0xFFFFFFFFCCCCD000|- rs1_val==3689348814741910324<br>                                                                                                                                                                                               |[0x80000cc4]:sllw a2, a0, a1<br> [0x80000cc8]:sd a2, 752(t0)<br>     |
| 112|[0x80003388]<br>0xFFFFFFFFE0000000|- rs1_val==7378697629483820647<br>                                                                                                                                                                                               |[0x80000cf0]:sllw a2, a0, a1<br> [0x80000cf4]:sd a2, 760(t0)<br>     |
| 113|[0x80003390]<br>0x0000000057D86670|- rs1_val==-3037000498<br>                                                                                                                                                                                                       |[0x80000d0c]:sllw a2, a0, a1<br> [0x80000d10]:sd a2, 768(t0)<br>     |
| 114|[0x80003398]<br>0x0000000000000000|- rs1_val==3037000500<br>                                                                                                                                                                                                        |[0x80000d28]:sllw a2, a0, a1<br> [0x80000d2c]:sd a2, 776(t0)<br>     |
| 115|[0x800033a0]<br>0xFFFFFFFFFFFE0000|- rs1_val == -524289<br>                                                                                                                                                                                                         |[0x80000d3c]:sllw a2, a0, a1<br> [0x80000d40]:sd a2, 784(t0)<br>     |
| 116|[0x800033a8]<br>0xFFFFFFFFFFE00000|- rs1_val == -1048577<br>                                                                                                                                                                                                        |[0x80000d50]:sllw a2, a0, a1<br> [0x80000d54]:sd a2, 792(t0)<br>     |
| 117|[0x800033b0]<br>0xFFFFFFFFFFFC0000|- rs1_val == -2097153<br>                                                                                                                                                                                                        |[0x80000d64]:sllw a2, a0, a1<br> [0x80000d68]:sd a2, 800(t0)<br>     |
| 118|[0x800033b8]<br>0xFFFFFFFFFFFC0000|- rs1_val == -4194305<br>                                                                                                                                                                                                        |[0x80000d78]:sllw a2, a0, a1<br> [0x80000d7c]:sd a2, 808(t0)<br>     |
| 119|[0x800033c0]<br>0xFFFFFFFFFEFFFFFE|- rs1_val == -8388609<br>                                                                                                                                                                                                        |[0x80000d8c]:sllw a2, a0, a1<br> [0x80000d90]:sd a2, 816(t0)<br>     |
| 120|[0x800033c8]<br>0xFFFFFFFFFEFFFFFF|- rs1_val < 0 and rs2_val == 0<br> - rs1_val == -16777217<br>                                                                                                                                                                    |[0x80000da0]:sllw a2, a0, a1<br> [0x80000da4]:sd a2, 824(t0)<br>     |
| 121|[0x800033d0]<br>0xFFFFFFFFFFFFE000|- rs1_val == -33554433<br>                                                                                                                                                                                                       |[0x80000db4]:sllw a2, a0, a1<br> [0x80000db8]:sd a2, 832(t0)<br>     |
| 122|[0x800033d8]<br>0xFFFFFFFFFFE00000|- rs1_val == -67108865<br>                                                                                                                                                                                                       |[0x80000dc8]:sllw a2, a0, a1<br> [0x80000dcc]:sd a2, 840(t0)<br>     |
| 123|[0x800033e0]<br>0x000000007FFFFFF0|- rs1_val == -134217729<br>                                                                                                                                                                                                      |[0x80000ddc]:sllw a2, a0, a1<br> [0x80000de0]:sd a2, 848(t0)<br>     |
| 124|[0x800033e8]<br>0xFFFFFFFFFFFFE000|- rs1_val == -268435457<br>                                                                                                                                                                                                      |[0x80000df0]:sllw a2, a0, a1<br> [0x80000df4]:sd a2, 856(t0)<br>     |
| 125|[0x800033f0]<br>0xFFFFFFFFFFFE0000|- rs1_val == -536870913<br>                                                                                                                                                                                                      |[0x80000e04]:sllw a2, a0, a1<br> [0x80000e08]:sd a2, 864(t0)<br>     |
| 126|[0x800033f8]<br>0xFFFFFFFFFFFFFC00|- rs1_val == -1073741825<br>                                                                                                                                                                                                     |[0x80000e18]:sllw a2, a0, a1<br> [0x80000e1c]:sd a2, 872(t0)<br>     |
| 127|[0x80003400]<br>0xFFFFFFFFFFFFFFF8|- rs1_val == -2147483649<br>                                                                                                                                                                                                     |[0x80000e30]:sllw a2, a0, a1<br> [0x80000e34]:sd a2, 880(t0)<br>     |
| 128|[0x80003408]<br>0xFFFFFFFFFFFFFE00|- rs1_val == -4294967297<br>                                                                                                                                                                                                     |[0x80000e48]:sllw a2, a0, a1<br> [0x80000e4c]:sd a2, 888(t0)<br>     |
| 129|[0x80003410]<br>0xFFFFFFFFFFFFFE00|- rs1_val == -8589934593<br>                                                                                                                                                                                                     |[0x80000e60]:sllw a2, a0, a1<br> [0x80000e64]:sd a2, 896(t0)<br>     |
| 130|[0x80003418]<br>0xFFFFFFFFF8000000|- rs1_val == -17179869185<br>                                                                                                                                                                                                    |[0x80000e78]:sllw a2, a0, a1<br> [0x80000e7c]:sd a2, 904(t0)<br>     |
| 131|[0x80003420]<br>0xFFFFFFFFFF800000|- rs1_val == -34359738369<br>                                                                                                                                                                                                    |[0x80000e90]:sllw a2, a0, a1<br> [0x80000e94]:sd a2, 912(t0)<br>     |
| 132|[0x80003428]<br>0xFFFFFFFFFFFFFFFC|- rs1_val == -68719476737<br>                                                                                                                                                                                                    |[0x80000ea8]:sllw a2, a0, a1<br> [0x80000eac]:sd a2, 920(t0)<br>     |
| 133|[0x80003430]<br>0xFFFFFFFFFF800000|- rs1_val == -137438953473<br>                                                                                                                                                                                                   |[0x80000ec0]:sllw a2, a0, a1<br> [0x80000ec4]:sd a2, 928(t0)<br>     |
| 134|[0x80003438]<br>0xFFFFFFFFFFFFE000|- rs1_val == -274877906945<br>                                                                                                                                                                                                   |[0x80000ed8]:sllw a2, a0, a1<br> [0x80000edc]:sd a2, 936(t0)<br>     |
| 135|[0x80003440]<br>0xFFFFFFFFFFFFFFE0|- rs1_val == -549755813889<br>                                                                                                                                                                                                   |[0x80000ef0]:sllw a2, a0, a1<br> [0x80000ef4]:sd a2, 944(t0)<br>     |
| 136|[0x80003448]<br>0xFFFFFFFFFFFFFFC0|- rs1_val == -1099511627777<br>                                                                                                                                                                                                  |[0x80000f08]:sllw a2, a0, a1<br> [0x80000f0c]:sd a2, 952(t0)<br>     |
| 137|[0x80003450]<br>0xFFFFFFFFFFFFF000|- rs1_val == -2199023255553<br>                                                                                                                                                                                                  |[0x80000f20]:sllw a2, a0, a1<br> [0x80000f24]:sd a2, 960(t0)<br>     |
| 138|[0x80003458]<br>0xFFFFFFFFFFFFFF80|- rs1_val == -4398046511105<br>                                                                                                                                                                                                  |[0x80000f38]:sllw a2, a0, a1<br> [0x80000f3c]:sd a2, 968(t0)<br>     |
| 139|[0x80003460]<br>0xFFFFFFFFFF800000|- rs1_val == -8796093022209<br>                                                                                                                                                                                                  |[0x80000f50]:sllw a2, a0, a1<br> [0x80000f54]:sd a2, 976(t0)<br>     |
| 140|[0x80003468]<br>0xFFFFFFFF80000000|- rs1_val == -17592186044417<br>                                                                                                                                                                                                 |[0x80000f68]:sllw a2, a0, a1<br> [0x80000f6c]:sd a2, 984(t0)<br>     |
| 141|[0x80003470]<br>0xFFFFFFFFFFFFFFF0|- rs1_val == -35184372088833<br>                                                                                                                                                                                                 |[0x80000f80]:sllw a2, a0, a1<br> [0x80000f84]:sd a2, 992(t0)<br>     |
| 142|[0x80003478]<br>0xFFFFFFFFE0000000|- rs1_val == -70368744177665<br>                                                                                                                                                                                                 |[0x80000f98]:sllw a2, a0, a1<br> [0x80000f9c]:sd a2, 1000(t0)<br>    |
| 143|[0x80003480]<br>0xFFFFFFFFFFFF0000|- rs1_val == -281474976710657<br>                                                                                                                                                                                                |[0x80000fb0]:sllw a2, a0, a1<br> [0x80000fb4]:sd a2, 1008(t0)<br>    |
| 144|[0x80003488]<br>0xFFFFFFFFFFFFFFC0|- rs1_val == -562949953421313<br>                                                                                                                                                                                                |[0x80000fc8]:sllw a2, a0, a1<br> [0x80000fcc]:sd a2, 1016(t0)<br>    |
| 145|[0x80003490]<br>0xFFFFFFFFFFFFE000|- rs1_val == -1125899906842625<br>                                                                                                                                                                                               |[0x80000fe0]:sllw a2, a0, a1<br> [0x80000fe4]:sd a2, 1024(t0)<br>    |
| 146|[0x80003498]<br>0xFFFFFFFFFFFFFFFE|- rs1_val == -2251799813685249<br>                                                                                                                                                                                               |[0x80000ff8]:sllw a2, a0, a1<br> [0x80000ffc]:sd a2, 1032(t0)<br>    |
| 147|[0x800034a0]<br>0xFFFFFFFFFFFC0000|- rs1_val == -4503599627370497<br>                                                                                                                                                                                               |[0x80001010]:sllw a2, a0, a1<br> [0x80001014]:sd a2, 1040(t0)<br>    |
| 148|[0x800034a8]<br>0xFFFFFFFFC0000000|- rs1_val == -9007199254740993<br>                                                                                                                                                                                               |[0x80001028]:sllw a2, a0, a1<br> [0x8000102c]:sd a2, 1048(t0)<br>    |
| 149|[0x800034b0]<br>0xFFFFFFFFFFFFC000|- rs1_val == -18014398509481985<br>                                                                                                                                                                                              |[0x80001040]:sllw a2, a0, a1<br> [0x80001044]:sd a2, 1056(t0)<br>    |
| 150|[0x800034d0]<br>0x0000000010000000|- rs1_val == 4194304<br>                                                                                                                                                                                                         |[0x80001090]:sllw a2, a0, a1<br> [0x80001094]:sd a2, 1088(t0)<br>    |
