# Ascii-Earth-Powershell
Cool little ascii sphere, you can map ascii textures to (:

```
Param($t)
$t = $t -split "`n"
$mW = $t[0].Length - 1
$mH = $t.Length - 1
$SphR = 8
$sin = @(for ($i = 0; $i -lt 1000; $i += 1) { [Math]::Sin($i * 0.006283185307179) })
$cos = @(for ($i = 0; $i -lt 1000; $i += 1) { [Math]::Cos($i * 0.006283185307179) })
$R = New-Object System.Random
$strs = @()
for ($i = 0; $i -lt 10; $i++) {$str = @{x = $R.next(1,80);y = $R.next(1,40);s = $R.next(1,5)};$strs += $str}
[system.console]::title = "Ascii Earth - Made by JH1SC"
[void][System.Console]::SetWindowSize(80, 44)
Clear-Host
# Animation loop
while ($true) {
    $oA = (' ' * 3520).ToCharArray()
    foreach ($str in $strs) {$str.x = ($str.x - $str.s) % 80;$oA[($str.x + 80 * $str.y)] = "o"}
    $aY = 0
    while ($aY -lt 6.28) {
        $aX = 0
        while ($aX -lt 6.28) {
            $x = $SphR * $sin[($aY % 6.28 * 159.15)] * $cos[($aX % 6.28 * 159.15)]
            $y = $SphR * $sin[($aY % 6.28 * 159.15)] * $sin[($aX % 6.28 * 159.15)]
            $z = $SphR * $cos[($aY % 6.28 * 159.15)]
            $SaX = [Math]::Atan2($x, $z)
            $SaY = [Math]::Atan2(-$y, [Math]::Sqrt($x * $x + $z * $z))
            $Co= [int](($SaX / (2 * [Math]::PI) + 0.5) * $mW)
            $Ro = [int]((($SaY / [Math]::PI) + 0.5) * $mH)
            if ($Ro -ge 0 -and $Ro -lt $mH - 1 -and $Co -ge 0 -and $Co -lt $mW - 1) {$aC = $t[$Ro][$Co]}
            $xRX = $x * $cos[($aA % 6.28 * 159.15)] + $z * $sin[($aA % 6.28 * 159.15)]
            $zRX = - $x * $sin[($aA % 6.28 * 159.15)] + $z * $cos[($aA % 6.28 * 159.15)]
            $x = $xRX
            $z = $zRX
            $iD = 1 / 10
            $sX = [int](40 + 30 * $iD * $x); 
            $sY = [int](20 - 15 * $iD * $y); 
            if ($z -gt 0) {
                $oA[($sX + 80 * $sY)] = $aC
            }
            $aX += 0.065
        }
        $aY += 0.065
    }
    $aA += 0.09
    
    [Console]::SetCursorPosition(0, 0)
    [console]::write([string]::join("", $oA))
}
```

$FancyEarth = "................................................................................................................................................
.........................................................,.,,...................................................................................
...........................,..<-.l.JJrJJ@c..<-JZddddddaadaadadMd.............JJZ,..............................l-1..............................
......................l/<,......,.<l,-ll.........-ddadddddaa@@Mr..............................r1..........1dMadaZadJ/...........................
.......rccccr-<<..l//<l<.-cJZZZ,.1Z-..J-.caMZ.....l<Zdaaaa@aZJ<................</ddM/...........<<.cZ-ZdddJJJdJZMaaMadZZda1JaZccdaJZaZrr,,l<-<,,
../..<rcaJZdJZZZdZJJcadddaaaadadaa@@Jl<..l-JJ--....rZda@......./Jc...........ZMMc.Zaad.,ddJJZZZrMdcaadadZdaJZdaaaadadaMMddZadaadaddMZdZZaM@aJZac
......1/dZJ<-,1/ZaaaadadZZdddaaaa@.......JMa........../...................r@a@@..rrr1JZaardZZddd@aaaddddddadJdaaaddddZddZdZZdaZaMddccJ..l<-l,...
.................../aaadddaddaaaMadJZ-l..rdZdZdc.....................,r,.../,/../dZZdadadZddZdJZ@aZZddMddZZJZZZZdddddaaaaMaaaac.......<dJ.......
.....................ZdddaaaadaaaddddaZc/ZdaaZZZJ1....................</,1dJJZJcJZddaaaMad@dZdZaM@ZadZJZJrcJMaZaadddaaaadMMaZdMZ,,..............
......................<JZZdZdddaMdMadaaMZ@ad@d,........................-rd/aaJMacZ@M-c-ccd....aaMZadaMadZMMdaadMaaaaaddd@MadarZ<................
......................-dadaZadaaaaMMaZadJad1.........................daac..../,,aad..-,.lad/.<@ZJdZJdcZMMM@MadaaaaaaaaM@MdJM....<...............
.......................rdMdddaMMMMd@aJZa@-...........................11-..,<.......-rZZ@Madd.,ZZZJJZZaaZJJJZaZddaaaaa@Zc..lr.../,...............
........................./ZJaaMaM@MdMa@c.............................rMMM@dJ/J..c<....ZdMMradadaMaaM@adadaaaaaaaa@Ma@@dd<...<...................
........................../lZaa@@......r...........................1aaaMaaddaadMaJcdZcradaaJ.ZMadZ@MJJaM@@@@@@JdMaZMMdJd,.......................
.............................,aM@......l..........................dddaadddMMaadZddaMaJ.,aaM@dJJ/...,JZMZda@dJdada@@MZJ-.,.......................
..............................ldaZ</r......1......................adMaadaMaaaaM@daaMdaa..aaaZZJ......1adaa....aMM@l.....,.......................
....................................dar..........................1aJZadaaaaaMaadZdaaaaZa<r@...........d@.......cdaZr....,.......................
......................................1,-<M,@d@-...................ddaM@dMa@@addZdaaaZZMJaaM,..........<.......c..........,.....................
........................................./@ZZZd@MJZ.......................1JMaMMaadZdZZa@a@...................1.r<....J<........................
........................................-@aaMMaZaZ@a........................d@MaaaZJadZ@a.......................d/.,Zd@.........................
........................................MMaddadadJZdcdJcZ....................ddZdddaadad.........................r......l.....Z@Jc..............
.........................................@ZaadJJdZaMZZdaa@...................1dddadadaac..................................1.....l..1............
..........................................aJJaaZdZdMJdMM/....................JaaaaadMaM@....................................c@l..,..............
............................................da@a@cZMdaZ@.....................daaaaada@c...c@.............................cadaZa@drJ.............
............................................r@@MMJaZdJc.......................Jaadad@a...<M..........................<caddddda@@@ddM,...........
............................................d@@MaZZa/.........................rdaddd@.................................daaaMaM@dZZdMMal..........
............................................@d@ada@............................<aM@d..................................-a@MJl./acZaZc@...........
...........................................-@@@da...............................................................................cZcd............
..........................................,aaM<...................................................................................l..........<l.
..........................................1dMl.............................................................................................c....
..........................................r@1...................................................................................................
............................................l...................................................................................................
................................................................................................................................................
...............................................l................................................................................................
...........................................<,/r......................................,..1cJJZdZZZZaZ...-JJZdddddddMdddZZddddddddadJr/1l.........
.......................l..l....lJrrrc1ll1-1rrZ@r..................rcZZdZdddaaaMdJddadddaaacrJaaaaddJZJr..cZdaaZdZZMJ1adZaMadadl-daaaaaaM@@-.....
.........,rdcJdMMMaaadaaddaddJZZdadddaZr/...........</,...rdZZMaMMaadJJZcrr-l...rcJddddcr-...-1l...........JdaaaaaaaaaaadcrrJad<1JaaaaM@@1......
...........,,.,,,ll<<,<llllllll<l<ll,llllll.........,...,,,ll,,lll...,.....l,..................................,llllllllll<lllllllllllll........
................................................................................................................................................"

$BlandEarth = "............................................................................................................................................
............................................................................................................................................
..................................+++++++..+++++++++++++++++++..............................................................................
......................+.+++++..+.+.+++++........++++++++++++++.............................+..........++++++++++++++..+.....++..............
......++++++++++++++++++++++++++++++++..++++.....++++++++++.................++++++++.....+++++++++++++++++++++++++++++++++++++++++++++++++++
......+++++++++++++++++++++++++++++.....++++......++++...................++++.+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++.
........++.......+++++++++++++++++......++++++......................+....++++..++++++++++++++++++++++++++++++++++++++++++++++......++.......
....................++++++++++++++++++.+++++++++....................++..++++++++++++++++++++++++++++++++++++++++++++++++++++.......+........
......................+++++++++++++++++++++++........................+++++++++++++++++++++++++++++++++++++++++++++++++++++++................
......................+++++++++++++++++++++........................++++...+.+++++....++++.+++++++++++++++++++++++++++++++...................
......................+++++++++++++++++++..........................+++........+..++++++++..+++++++++++++++++++++++++...+....+...............
.........................++++++++++++++............................+++++++++..+....++++++++++++++++++++++++++++++++++.......................
..........................++++++......+..........................++++++++++++++++++++++++++++++++++++++++++++++++++++.......................
.............................+++................................++++++++++++++++++++.++++++++....+++++++++++++++++..........................
...............................++.++............................+++++++++++++++++++++.+++++.......++++.....+++++............................
....................................++..........................+++++++++++++++++++++++++..........++.......+.++............................
........................................+++++++..................++++++++++++++++++++++++...................................................
.......................................+++++++++++........................++++++++++++++.....................+...+++........................
.......................................++++++++++++++++...................++++++++++++.......................++..++........++...............
.......................................+++++++++++++++++...................++++++++++.......................................++..............
........................................+++++++++++++++....................+++++++++++..................................+++..+..............
..........................................+++++++++++++....................+++++++++...++............................++++++++++.............
...........................................+++++++++........................++++++++...+..........................+++++++++++++++...........
..........................................+++++++++.........................++++++................................+++++++++++++++...........
..........................................+++++++............................+++...................................+++....+++++++...........
..........................................++++................................................................................+.............
.........................................++++...............................................................................................
.........................................+++................................................................................................
............................................................................................................................................
............................................................................................................................................
............................................................................................................................................
............................................++.....................................+.++++++++++++..+++++++++++++++++++++++++++++++++........
....................+++++++...++++++++++++++++.................+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++......
..........+++++++++++++++++++++++++++++++..........+....+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++......."

$jh1sc = ".....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
............a@@@@@@@a......M@@@c.....aM@@<........-aM@J........aM@@@@@@MM........../aM@@@@@@al.......
............a@@@@MM@a......@Ma@a.....@@M@a.....a@@@@@@d.......aaMMMMM@@@@J.......aM@@@M@@@@@@a.......
...............-aMMMa......MMMMc....-MMM@a.....ZMMMMMa-.......@MMMMal...........,@MM@aa---/aa,.......
................aMMMM-.....MMMM@@@MM@MMM@a.......<aMMa........a@MMM@@@MJZ.......a@MMa<...............
................aMaMa......@MaMM@@@@@MaM@a.......-aaMa.........<aM@@@@@@MM,.....@MMaa................
......M@@@a,....aMM@a......MMMMad-,-a@MMMa.......,aMMa...............-aMM@a.....aMMaa................
......aMMa@MaaaaMM@@.......MMM@a....,MMaaa......1aMMMMa-......a@Ma/1aaMaM@a......MM@@MaaZdaMaJ.......
.......a@@@@@@@@@@M.......-@@@@a.....M@@Ma.....a@@@@@@@@Z.....@@@@@@@@@@@@........aM@@@@@@@@@M.......
..........aMMaM@a..........<-ac.......aar.......daaMaaa/......l,1aaaMMa-.............aaaaaa-.........
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
.....................................................................................................
....................................................................................................."













