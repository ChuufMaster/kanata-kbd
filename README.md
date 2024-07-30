# Config

```lisp

;; Kanata configuration for caps to esc+ctrl

(defcfg
  process-unmapped-keys yes
)

(defsrc
  f12
  caps   a   s   d   f  h  j   k   l   ;
                     v
)

(defvar
  ;; Note: consider using different time values for your different fingers.
  ;; For example, your pinkies might be slower to release keys and index
  ;; fingers faster.
  tap-time 200
  hold-time 150

  left-hand-keys (
    q w e r t
    a s d f g
    z x c v b
  )
  right-hand-keys (
    y u i o p
    h j k l ;
    n m , . /
  )
)

(deflayer base
  @f12
  @caps  @a  @s  @d  @f  h  @j  @k  @l  @;
                        @v
)

(deflayer nomods
  @f12
  @caps  a   s   d   f  h  j   k   l   ;
                        v
)

(deflayer arrows-while-held
  @f12
  lrld  a   s   d   f  left down up rght ;
                        v
)

(deflayer super-layer
  @f12
  @caps     a   s   d   f  left down up rght ;
                       v
)

(deflayer alt-layer
  @f12
  @caps a  s  d  f  left down up rght ;
                 v
)

(deflayer game-layer
  @f12-game
  @caps a s d f h j k l ;
              v
)

(deffakekeys
  to-base (layer-switch base)
)

(defalias
  tap (multi
    (layer-switch nomods)
    (on-idle-fakekey to-base tap 20)
  )

  arws (layer-while-held arrows-while-held)

  super-uses (layer-while-held super-layer)

  alt-uses (layer-while-held alt-layer)

  f12 (layer-switch game-layer)
  f12-game (layer-switch base)

  caps (tap-hold-press $tap-time $hold-time esc (multi lctrl @tap))
  a (tap-hold-release-keys $tap-time $hold-time (multi a @tap) (multi lmet @super-uses) $left-hand-keys)
  s (tap-hold-release-keys $tap-time $hold-time (multi s @tap) (multi lalt @alt-uses) $left-hand-keys)
  d (tap-hold-release-keys $tap-time $hold-time (multi d @tap) lctl $left-hand-keys)
  f (tap-hold-release-keys $tap-time $hold-time (multi f @tap) lsft $left-hand-keys)
  j (tap-hold-release-keys $tap-time $hold-time (multi j @tap) rsft $right-hand-keys)
  k (tap-hold-release-keys $tap-time $hold-time (multi k @tap) rctl $right-hand-keys)
  l (tap-hold-release-keys $tap-time $hold-time (multi l @tap) ralt $right-hand-keys)
  ; (tap-hold-release-keys $tap-time $hold-time (multi ; @tap) rmet $right-hand-keys)
  v (tap-hold-release $tap-time $hold-time v @arws)
)

;; ___A___ ___S___ ___D___ ___F___ ___J___ ___K___ ___L___ ___;___
;; __lmet___lalt___lctl___lsft_ __rsft___rclt___ralt___rmet_

```
