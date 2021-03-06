
# Table of Contents

1.  [Lakota Input Modes for Emacs](#orged787e4)
    1.  [White Hat Orthography](#org8b942ee)
    2.  [Suggested Lakota Orthography](#orgd472618)
2.  [Lakota X11 Keyboard Layouts](#org87b82b9)

Haú, mitákuyepi.
Grant Shoshín Shangreaux emáčiyapi.

Blóketu k'uŋ héhaŋ, Lakota Summer Institute ektá waí.
Pispíza waŋ wayáwa iyáye. Wamákȟaškaŋ waŋzí waŋbláke.


<a id="orged787e4"></a>

# Lakota Input Modes for Emacs

Keyboard inputs for the Lakota language created with Emacs' `quail` package.

To use these input modes, put the `lakota-input.el` file in your load path
and `(require 'lakota-input)`, or simply evaluate the quail package you
wish to add. In Emacs, `C-\` will let you select an input mode, and toggle
it once you have. If you wish to use a different one, use `C-u C-\`


<a id="org8b942ee"></a>

## White Hat Orthography

This orthography was developed by Lakota people in 1982 and used in
Albert White Hat's book "Reading and Writing the Lakota Language".

Currently, this just maps the "f" key to the nasal ŋ and the "r" and
"v" keys are mapped to combining dot above (ċ), and combining macron (line)
above (t̄). To use them, type the letter followed by the combining diacritic
you wish to use.

    (quail-define-package
    "white-hat" "Lakota" "Lak " t
    "Input method for the White Hat orthography."
    nil t nil nil nil nil nil nil nil nil t)
    
    (quail-define-rules
     ("f" ?ŋ)
     ("r" #x307)                            ; COMBINING DOT ABOVE
     ("v" #x304)                            ; COMBINING MACRON
     )


<a id="orgd472618"></a>

## Suggested Lakota Orthography

This orthography was developed by the Lakota Language Consortium, and
is used in their teaching materials such as the New Lakota Dictionary.

    (quail-define-package
     "lakota-slo" "Lakota" "Lak " t
     "Input method for the Suggested Lakota Orthography.
    Uses a postfix modifier key for adding accent diacritics. To add stress
    to a vowel, simply type the single quote ' after the vowel. All other
    characters are bound to a single key. Mitákuyepi philámayaye ló."
    nil t nil nil nil nil nil nil nil nil t)
    
    (quail-define-rules
     ;; accented vowels
     ("a'" ?á) ("A'" ?Á)
     ("e'" ?é) ("E'" ?É)
     ("i'" ?í) ("I'" ?Í)
     ("o'" ?ó) ("O'" ?Ó)
     ("u'" ?ú) ("U'" ?Ú)
     ;; consonants with hacek (wedges)
     ("c" ?č) ("C" ?Č)
     ("j" ?ȟ) ("J" ?Ȟ)
     ("q" ?ǧ) ("Q" ?Ǧ)
     ("x" ?ž) ("X" ?Ž)
     ("r" ?š) ("R" ?Š)
     ;; velar nasal n
     ("f" ?ŋ))
     ;; glottal stop
     ("''" ?’)
    
    (provide 'lakota-input)


<a id="org87b82b9"></a>

# Lakota X11 Keyboard Layouts

The layout definitions are in the `lakota` file in this repo. They are
essentially the same as the Emacs layouts above, except that the 
combining accent is a prefix. Type ' followed by the vowel.

To "install" the layouts, I put the `lakota` file at `/usr/share/X11/xkb/symbols`
and then added this XML section to `/usr/share/X11/xkb/rules/evdev.xml` in the
appropriate section:

    <layout>
      <configItem>
        <name>lakota</name>
        <description>Lakota</description>
      </configItem>
      <variantList>
        <variant>
          <configItem>
            <name>whitehat</name>
            <shortDescription>lwh</shortDescription>
            <description>Lakota White Hat</description>
          </configItem>
        </variant>
      </variantList>
      <variantList>
        <variant>
          <configItem>
            <name>slo</name>
            <shortDescription>slo</shortDescription>
            <description>Suggested Lakota Orthography</description>
          </configItem>
        </variant>
      </variantList>
    </layout>

Once that is done and you restart X, you should see the Lakota keyboard layout
available in your keyboard settings.

