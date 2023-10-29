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

