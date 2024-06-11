# picoCTF writeup
## 1) Flags

### Description:
> What do the flags mean?
<img width="821" alt="flag" src="https://github.com/saanvivi/picoCTF-writeup/assets/145047724/5db9ab53-c5c6-443a-9e5d-30c14e8f5865">
<p> Feeeling very confused initially, I tried deciphering the flags myself. Knowing the format picoCTF{}, I figured some letters but couldnt make sense of it. I googled "flag cipher" which lead me to the International maritime signal flags. So i was able to decode the flag. </p>

The flag is `picoCTF{F1AG5AND5TUFF}`

## 2) miniRSA

### Description:
> Let's decrypt this: ciphertext? Something seems a bit small.
~~~
N: 29331922499794985782735976045591164936683059380558950386560160105740343201513369939006307531165922708949619162698623675349030430859547825708994708321803705309459438099340427770580064400911431856656901982789948285309956111848686906152664473350940486507451771223435835260168971210087470894448460745593956840586530527915802541450092946574694809584880896601317519794442862977471129319781313161842056501715040555964011899589002863730868679527184420789010551475067862907739054966183120621407246398518098981106431219207697870293412176440482900183550467375190239898455201170831410460483829448603477361305838743852756938687673
e: 3

ciphertext (c): 2205316413931134031074603746928247799030155221252519872649649212867614751848436763801274360463406171277838056821437115883619169702963504606017565783537203207707757768473109845162808575425972525116337319108047893250549462147185741761825125 
~~~
<p> We know that <b>c = m^e mod n</b>. <br> After extensive research, i found out that because e is very small, the mod doesnt come into the picture, meaning c = m^e. Thus, to find the answer all you have to do is take the cube root of c. While doing so using a python program i faced trouble as c is very large. i got over this by converting the soln to hex. I then converted the hex to ASCII to get the flag </p>

~~~
c=2205316413931134031074603746928247799030155221252519872649649212867614751848436763801274360463406171277838056821437115883619169702963504606017565783537203207707757768473109845162808575425972525116337319108047893250549462147185741761825125
def cubic_root(n):
    a = 1
    b = n
    while b - a > 1:
        mid = (a + b) // 2
        if mid**3 > n:
            b = mid
        else:
            a = mid

    if a ** 3 == n:
        return a
    elif b ** 3 == n:
        return b
    else:
        return 0

m = cubic_root(c)
h = hex(m)
print(h)
~~~
The flag is `picoCTF{n33d_a_lArg3r_e_606ce004}`

## 3) transposition-trial
### Description:
>Our data got corrupted on the way here. Luckily, nothing got replaced, but every block of 3 got scrambled around! The first word seems to be three letters long, maybe you can use that to recover the rest of the message.
Download the corrupted message here.
~~~
heTfl g as iicpCTo{7F4NRP051N5_16_35P3X51N3_V6E5926A}4
~~~
As the description suggests, every block of three got scrambled around. Figuring that the first few words are "The flag is", it was easy to notice that for every block, the last letter is to be made the first to unscramble it. This bring us to the flag.

The flag is `picoCTF{7R4N5P051N6_15_3XP3N51V3_56E6924A}`

## 4) substitution attack 1
### Description:
> A second message has come in the mail, and it seems almost identical to the first one. Maybe the same thing will work again.
Download the message here.
~~~
SYTe (eakdy tkd sjbyndr yar thjm) jdr j yobr kt skxbnyrd ersndzyo skxbryzyzkc. Skcyreyjcye jdr bdrercyrq gzya j ery kt sajhhrcmre gazsa yrey yarzd sdrjyzwzyo, yrsaczsjh (jcq mkkmhzcm) evzhhe, jcq bdklhrx-ekhwzcm jlzhzyo. Sajhhrcmre nenjhho skwrd j cnxlrd kt sjyrmkdzre, jcq garc ekhwrq, rjsa ozrhqe j eydzcm (sjhhrq j thjm) gazsa ze enlxzyyrq yk jc kchzcr eskdzcm erdwzsr. SYTe jdr j mdrjy gjo yk hrjdc j gzqr jddjo kt skxbnyrd ersndzyo evzhhe zc j ejtr, hrmjh rcwzdkcxrcy, jcq jdr akeyrq jcq bhjorq lo xjco ersndzyo mdknbe jdkncq yar gkdhq tkd tnc jcq bdjsyzsr. Tkd yaze bdklhrx, yar thjm ze: bzskSYT{TD3UN3CSO_4774SV5_4D3_S001_7JJ384LS}
~~~
Analyzing the punctuations and the text, i figured out the first and last sentences. Theyre "CTFs (short for capture the flag)..." and "For this problem, the flag is: picoCTF{...}"
Through this i figured out most of the substitutions in the flag. I guessed the remaining letters, knowing numbers dont change. The hint regarding frequency attacks helped.

The flag is `picoCTF{FR3QU3NCY_4774CK5_4R3_C001_7AA384BC}`

## 5) Dachshund Attack
### Description:
> What if d is too small? Connect with nc mercury.picoctf.net 37455.

First i found that when d is small, Wiener attacks work when d is small. <br>
i used `nc mercury.picoctf.net 37455` and got the values as shown
~~~
Welcome to my RSA challenge!
e: 120637597584146241111653531031311742875916622608508948388416240765451525050131914389034120734963104644703191211239560567330474309393462011268263891618847097118033915670897143579105785190576962149381041979764269754548294764427645432285780085184775714758772166259687730831759895911715135162819460943760246706961
n: 171915523646511714734988373688339529908867194882070416439491032421419221257251741163385436968386761578973062954886630199219587017997347075463397783274775327770699761004049198827637910978575434240304392665393342413834449695041860030610577555003476770139036488058715994013034962013055918793775828896013431387919
c: 37369065384754936167310355955845840505349299513100657454287076735598972372106690028877705995633722440380415602771849138951669066867914005747458073909340575683655325551369380225649929864285847308747185976414876285046410066626953229226573782733155715774656359772538081091777913009811584403803839363533952332667
~~~
I looked online and found a [program](https://github.com/orisano/owiener) to carry out a Wiener attack. <br>
~~~
import owiener

e = 120637597584146241111653531031311742875916622608508948388416240765451525050131914389034120734963104644703191211239560567330474309393462011268263891618847097118033915670897143579105785190576962149381041979764269754548294764427645432285780085184775714758772166259687730831759895911715135162819460943760246706961
n = 171915523646511714734988373688339529908867194882070416439491032421419221257251741163385436968386761578973062954886630199219587017997347075463397783274775327770699761004049198827637910978575434240304392665393342413834449695041860030610577555003476770139036488058715994013034962013055918793775828896013431387919
d = owiener.attack(e, n)

if d is None:
    print("Failed")
else:
    print("Hacked d={}".format(d))
~~~
d=35238064561695282799647947362811227714296700106386796052429037996303465227161
Thus, n,e,d and c are all known. I put these values in [dcode](https://www.dcode.fr/rsa-cipher) and got the flag

The flag is `picoCTF{proving_wiener_3878674}`
