# Q. substitution attack 1
### Description:
> A second message has come in the mail, and it seems almost identical to the first one. Maybe the same thing will work again.
Download the message here.
~~~
SYTe (eakdy tkd sjbyndr yar thjm) jdr j yobr kt skxbnyrd ersndzyo skxbryzyzkc. Skcyreyjcye jdr bdrercyrq gzya j ery kt sajhhrcmre gazsa yrey yarzd sdrjyzwzyo, yrsaczsjh (jcq mkkmhzcm) evzhhe, jcq bdklhrx-ekhwzcm jlzhzyo. Sajhhrcmre nenjhho skwrd j cnxlrd kt sjyrmkdzre, jcq garc ekhwrq, rjsa ozrhqe j eydzcm (sjhhrq j thjm) gazsa ze enlxzyyrq yk jc kchzcr eskdzcm erdwzsr. SYTe jdr j mdrjy gjo yk hrjdc j gzqr jddjo kt skxbnyrd ersndzyo evzhhe zc j ejtr, hrmjh rcwzdkcxrcy, jcq jdr akeyrq jcq bhjorq lo xjco ersndzyo mdknbe jdkncq yar gkdhq tkd tnc jcq bdjsyzsr. Tkd yaze bdklhrx, yar thjm ze: bzskSYT{TD3UN3CSO_4774SV5_4D3_S001_7JJ384LS}
~~~
Analyzing the punctuations and the text, i figured out the first and last sentences. Theyre "CTFs (short for capture the flag)..." and "For this problem, the flag is: picoCTF{...}"
Through this i figured out most of the substitutions in the flag. I guessed the remaining letters, knowing numbers dont change. The hint regarding frequency attacks helped.

The flag is `picoCTF{FR3QU3NCY_4774CK5_4R3_C001_7AA384BC}`
