▼リスト4-1 Fyneを使ってみる

```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/widget"
)

func main() {
	a := app.New()
	w := a.NewWindow("Hello")
	w.SetContent(
		widget.NewLabel("Hello Fyne!"),
	)
	w.ShowAndRun()
}
```

▼リスト4-2 複数部品を並べる

```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/widget"
)

func main() {
	a := app.New()
	w := a.NewWindow("Hello")
	w.SetContent(
		// replaced(fyne v2): widget.Box -> container.NewH/VBox
		container.NewVBox(
			widget.NewLabel("Hello Fyne!"),
			widget.NewLabel("This is sample application!"),
		),
	)
	w.ShowAndRun()
}
```

▼リスト4-3 ボタンを使う

```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/widget"
	"strconv"
)

func main() {
	c := 0

	a := app.New()
	w := a.NewWindow("Hello")
	l := widget.NewLabel("Hello Fyne!")
	w.SetContent(
		// replaced(fyne v2): widget.Box -> container.NewH/VBox
		container.NewVBox(
			l,
			widget.NewButton("Click me!", func() {
				c++
				l.SetText("count: " + strconv.Itoa(c))
			}),
		),
	)
	w.ShowAndRun()
}
```

▼リスト4-4 エントリーで入力する

```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/widget"
	"strconv"
)

func main() {
	a := app.New()
	w := a.NewWindow("Hello")
	l := widget.NewLabel("Hello Fyne!")
	e := widget.NewEntry()
	e.SetText("0")
	w.SetContent(
		// replaced(fyne v2): widget.Box -> container.NewH/VBox
		container.NewVBox(
			l, e,
			widget.NewButton("Click me!", func() {
				n, _ := strconv.Atoi(e.Text)
				l.SetText("Total: " + strconv.Itoa(total(n)))
			}),
		),
	)
	w.ShowAndRun()
}

func total(n int) int {
	t := 0
	for i := 1; i <= n; i++ {
		t += i
	}
	return t
}
```

▼リスト4-5 ライトテーマに変更する

```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/theme"
	"fyne.io/fyne/v2/widget"
)

func main() {
	a := app.New()
	w := a.NewWindow("Hello")
	l := widget.NewLabel("Hello Fyne!")
	e := widget.NewEntry()
	e.SetText("0")
	w.SetContent(
		// replaced(fyne v2): widget.Box -> container.NewH/VBox
		container.NewVBox(
			l, e,
			widget.NewButton("Click me!", nil),
		),
	)
	a.Settings().SetTheme(theme.LightTheme())
	w.ShowAndRun()
}
```

▼リスト4-6 チェックボックスを利用する

```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/widget"
)

func main() {
	a := app.New()
	w := a.NewWindow("Hello")
	l := widget.NewLabel("Hello Fyne!")
	c := widget.NewCheck("Check!", func(f bool) {
		if f {
			l.SetText("CHECKED!!")
		} else {
			l.SetText("not checked.")
		}
	})
	c.SetChecked(true)
	w.SetContent(
		// replaced(fyne v2): widget.Box -> container.NewH/VBox
		container.NewVBox(
			l, c,
		),
	)
	w.ShowAndRun()
}
```

▼リスト4-7 ラジオボタンを利用する

```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/widget"
)

func main() {
	a := app.New()
	w := a.NewWindow("Hello")
	l := widget.NewLabel("Hello Fyne!")
	// replaced(fyne v2): widget.Radio -> widget.RadioGroup
	r := widget.NewRadioGroup(
		[]string{"One", "Two", "Three"},
		func(s string) {
			if s == "" {
				l.SetText("not selected.")
			} else {
				l.SetText("selected: " + s)
			}
		},
	)
	r.SetSelected("One")
	w.SetContent(
		// replaced(fyne v2): widget.Box -> container.NewH/VBox
		container.NewVBox(
			l, r,
		),
	)
	w.ShowAndRun()
}
```

▼リスト4-8 スライダーを利用する

```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/widget"
	"strconv"
)

func main() {
	a := app.New()
	w := a.NewWindow("Hello")
	l := widget.NewLabel("Hello Fyne!")
	s := widget.NewSlider(0.0, 100.)
	b := widget.NewButton("Check", func() {
		l.SetText("value: " + strconv.Itoa(int(s.Value)))
	})
	w.SetContent(
		// replaced(fyne v2): widget.Box -> container.NewH/VBox
		container.NewVBox(
			l, s, b,
		),
	)
	w.ShowAndRun()
}
```

▼リスト4-9 選択リストを利用する

```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/widget"
)

func main() {
	a := app.New()
	w := a.NewWindow("Hello")
	l := widget.NewLabel("Hello Fyne!")
	sl := widget.NewSelect(
		[]string{"Eins", "Twei", "Drei"},
		func(s string) {
			l.SetText("selected: " + s)
		},
	)
	w.SetContent(
		// replaced(fyne v2): widget.Box -> container.NewH/VBox
		container.NewVBox(
			l, sl,
		),
	)
	w.ShowAndRun()
}
```

▼リスト4-10 プログレスバーを使う

```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/widget"
)

func main() {
	v := 0.

	a := app.New()
	w := a.NewWindow("Hello")
	l := widget.NewLabel("Hello Fyne!")
	p := widget.NewProgressBar()
	b := widget.NewButton("Up!", func() {
		v += 0.1
		if v > 1.0 {
			v = 0.
		}
		p.SetValue(v)
	})
	w.SetContent(
		// replaced(fyne v2): widget.Box -> container.NewH/VBox
		container.NewVBox(
			l, p, b,
		),
	)
	w.ShowAndRun()
}
```

▼リスト4-11 フォームを利用する

```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/widget"
)

func main() {
	a := app.New()
	w := a.NewWindow("Hello")
	l := widget.NewLabel("Hello Fyne!")
	ne := widget.NewEntry()
	pe := widget.NewPasswordEntry()
	w.SetContent(
		// replaced(fyne v2): widget.Box -> container.NewH/VBox
		container.NewVBox(
			l,
			widget.NewForm(
				widget.NewFormItem("Name", ne),
				widget.NewFormItem("Pass", pe),
			),
			widget.NewButton("OK", func() {
				l.SetText(ne.Text + " & " + pe.Text)
			}),
		),
	)
	w.ShowAndRun()
}
```

▼リスト4-12 グループを利用する

```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/widget"
)

func main() {
	a := app.New()
	w := a.NewWindow("Hello")
	l := widget.NewLabel("Hello Fyne!")
	ck1 := widget.NewCheck("check 1", nil)
	ck2 := widget.NewCheck("check 2", nil)
	w.SetContent(
		// replaced(fyne v2): widget.Box -> container.NewH/VBox
		container.NewVBox(
			l,
			// replaced(fyne v2): widget.Group -> widget.NewCard
			widget.NewCard(
				"Group",
				"",
				container.NewVBox(ck1, ck2),
			),
			widget.NewButton("OK", func() {
				re := "result: "
				if ck1.Checked {
					re += "Check-1 "
				}
				if ck2.Checked {
					re += "Check-2"
				}
				l.SetText(re)
			}),
		),
	)
	w.ShowAndRun()
}
```

▼リスト4-13 タブコンテナを利用する

```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/widget"
)

func main() {
	a := app.New()
	w := a.NewWindow("Hello")
	w.SetContent(
		// replaced(fyne v2): widget.Box -> container.NewH/VBox
		container.NewVBox(
			// replaced(fyne v2): widget.TabContainer -> container.AppTabs
			container.NewAppTabs(
				container.NewTabItem(
					"First",
					widget.NewLabel("This is First tab item."),
				),
				container.NewTabItem(
					"Second",
					widget.NewLabel("This is Second tab item."),
				),
			),
		),
	)
	w.ShowAndRun()
}
```

▼リスト4-14 BorderLayoutを利用する

```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/layout"
	"fyne.io/fyne/v2/widget"
)

func main() {
	a := app.New()
	w := a.NewWindow("Hello")
	bt := widget.NewButton("Top", nil)
	bb := widget.NewButton("Bottom", nil)
	bl := widget.NewButton("Left", nil)
	br := widget.NewButton("Right", nil)
	w.SetContent(
		// deprecated(fyne v2): fyne.NewContainerWithLayout -> container.New
		container.New(
			layout.NewBorderLayout(
				bt, bb, bl, br,
			),
			bt, bb, bl, br,
			widget.NewLabel("Center."),
		),
	)
	w.ShowAndRun()
}
```

▼リスト4-15 GridLayoutを利用する

```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/layout"
	"fyne.io/fyne/v2/widget"
)

func main() {
	a := app.New()
	w := a.NewWindow("Hello")
	w.SetContent(
		// deprecated(fyne v2): fyne.NewContainerWithLayout -> container.New
		container.New(
			layout.NewGridLayout(3),
			widget.NewButton("One", nil),
			widget.NewButton("Two", nil),
			widget.NewButton("Three", nil),
			widget.NewButton("Four", nil),
			layout.NewSpacer(),
			widget.NewButton("Five", nil),
			widget.NewButton("Six", nil),
			layout.NewSpacer(),
			widget.NewButton("Seven", nil),
			widget.NewButton("Eight", nil),
			widget.NewButton("Nine", nil),
			widget.NewButton("Ten", nil),
		),
	)
	w.ShowAndRun()
}
```

▼リスト4-16 スクロールコンテナを利用する

```go
package main

import (
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/widget"
)

func main() {
	a := app.New()
	w := a.NewWindow("Hello")
	w.SetContent(
		// replaced(fyne v2): widget.ScrollContainer -> container.Scroll
		container.NewScroll(
			// replaced(fyne v2): widget.Box -> container.NewH/VBox
			container.NewVBox(
				widget.NewButton("One", nil),
				widget.NewButton("Two", nil),
				widget.NewButton("Three", nil),
				widget.NewButton("Four", nil),
				widget.NewButton("Five", nil),
				widget.NewButton("Six", nil),
				widget.NewButton("Seven", nil),
				widget.NewButton("Eight", nil),
				widget.NewButton("Nine", nil),
				widget.NewButton("Ten", nil),
			),
		),
	)
	w.ShowAndRun()
}
```

▼リスト4-17 テーマとウインドウサイズを調整する

```go
package main

import (
	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/theme"
	"fyne.io/fyne/v2/widget"
)

func main() {
	a := app.New()
	w := a.NewWindow("Hello")
	w.SetContent(
		// replaced(fyne v2): widget.ScrollContainer -> container.Scroll
		container.NewScroll(
			// replaced(fyne v2): widget.Box -> container.NewH/VBox
			container.NewVBox(
				widget.NewButton("One", nil),
				widget.NewButton("Two", nil),
				widget.NewButton("Three", nil),
				widget.NewButton("Four", nil),
				widget.NewButton("Five", nil),
				widget.NewButton("Six", nil),
				widget.NewButton("Seven", nil),
				widget.NewButton("Eight", nil),
				widget.NewButton("Nine", nil),
				widget.NewButton("Ten", nil),
			),
		),
	)
	a.Settings().SetTheme(theme.LightTheme())
	w.Resize(fyne.NewSize(200, 200))
	w.ShowAndRun()
}
```

▼リスト4-18 ツールバーを実装する

```go
package main

import (
	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/layout"
	"fyne.io/fyne/v2/theme"
	"fyne.io/fyne/v2/widget"
)

func main() {
	a := app.New()
	w := a.NewWindow("Hello")
	l := widget.NewLabel("This is sample widget.")
	tb := widget.NewToolbar(
		widget.NewToolbarAction(theme.HomeIcon(), func() {
			l.SetText("Select Home Icon!")
		}),
		widget.NewToolbarAction(theme.InfoIcon(), func() {
			l.SetText("Select Information Icon!")
		}),
	)
	w.SetContent(
		// deprecated(fyne v2): fyne.NewContainerWithLayout -> container.New
		container.New(
			layout.NewBorderLayout(
				nil, tb, nil, nil,
			),
			l,
			tb,
		),
	)
	w.Resize(fyne.NewSize(300, 200))
	w.ShowAndRun()
}
```

▼リスト4-19 メニューバーを利用する

```go
package main

import (
	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/widget"
)

func main() {
	a := app.New()
	w := a.NewWindow("Hello")
	l := widget.NewLabel("Hello Fyne!")
	mm := fyne.NewMainMenu(
		fyne.NewMenu(
			"File",
			fyne.NewMenuItem("New", func() {
				l.SetText("select 'New' menu item.")
			}),
			fyne.NewMenuItem("Quit", func() {
				a.Quit()
			}),
		),
	)
	w.SetMainMenu(mm)
	w.SetContent(
		// replaced(fyne v2): widget.Box -> container.NewH/VBox
		container.NewVBox(
			l,
			widget.NewButton("ok", nil),
		),
	)
	w.Resize(fyne.NewSize(300, 200))
	w.ShowAndRun()
}
```

▼リスト4-20 アラートの表示

```go
package main

import (
	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/dialog"
	"fyne.io/fyne/v2/layout"
	"fyne.io/fyne/v2/theme"
	"fyne.io/fyne/v2/widget"
)

func main() {
	a := app.New()
	w := a.NewWindow("Hello")
	l := widget.NewLabel("Hello Fyne!")
	b := widget.NewButton("Click", func() {
		dialog.ShowInformation("Alert",
			"This is sample alert!", w)
	})
	w.SetContent(
		// deprecated(fyne v2): fyne.NewContainerWithLayout -> container.New
		container.New(
			layout.NewBorderLayout(
				nil, b, nil, nil,
			),
			l, b,
		),
	)
	//a.Settings().SetTheme(theme.LightTheme())
	w.Resize(fyne.NewSize(350, 250))
	w.ShowAndRun()
}

```

▼リスト4-21 ShowConfirmを利用する

```go
package main

import (
	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/dialog"
	"fyne.io/fyne/v2/layout"
	"fyne.io/fyne/v2/theme"
	"fyne.io/fyne/v2/widget"
)

func main() {
	a := app.New()
	w := a.NewWindow("Hello")
	l := widget.NewLabel("Hello Fyne!")
	b := widget.NewButton("Click", func() {
		dialog.ShowConfirm("Alert",
			"Please check 'YES'!",
			func(f bool) {
				if f {
					l.SetText("OK, thank you!!")
				} else {
					l.SetText("oh...")
				}
			}, w,
		)
	})
	w.SetContent(
		// deprecated(fyne v2): fyne.NewContainerWithLayout -> container.New
		container.New(
			layout.NewBorderLayout(
				nil, b, nil, nil,
			),
			l, b,
		),
	)
	//a.Settings().SetTheme(theme.LightTheme())
	w.Resize(fyne.NewSize(350, 250))
	w.ShowAndRun()
}
```

▼リスト4-22 テキスト入力ダイアログを表示する

```go
package main

import (
	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/dialog"
	"fyne.io/fyne/v2/layout"
	"fyne.io/fyne/v2/theme"
	"fyne.io/fyne/v2/widget"
)

func main() {
	a := app.New()
	w := a.NewWindow("Hello")
	l := widget.NewLabel("Hello Fyne!")
	e := widget.NewEntry()
	b := widget.NewButton("click", func() {
		dialog.ShowCustomConfirm("Enter message.", "OK",
			"Cancel", e, func(f bool) {
				if f {
					l.SetText("typed: '" + e.Text + "'.")
				} else {
					l.SetText("no message...")
				}
			}, w)
	})
	w.SetContent(
		// deprecated(fyne v2): fyne.NewContainerWithLayout -> container.New
		container.New(
			layout.NewBorderLayout(
				nil, b, nil, nil,
			),
			l, b,
		),
	)
	a.Settings().SetTheme(theme.LightTheme())
	w.Resize(fyne.NewSize(350, 250))
	w.ShowAndRun()
}
```

▼リスト4-23 MyEntryを作成する
※ この内容はリスト4-24に含まれています。

▼リスト4-24 MyEntryを利用する

```go
package main

import (
	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/widget"
)

type MyEntry struct {
	widget.Entry
	entered func(e *MyEntry)
}

func NewMyEntry(f func(e *MyEntry)) *MyEntry {
	e := &MyEntry{}
	e.ExtendBaseWidget(e)
	e.entered = f
	return e
}

func (e *MyEntry) KeyDown(key *fyne.KeyEvent) {
	switch key.Name {
	case fyne.KeyReturn, fyne.KeyEnter:
		e.entered(e)
	default:
		e.Entry.KeyDown(key)
	}
}

func main() {
	a := app.New()
	w := a.NewWindow("Hello")
	l := widget.NewLabel("Hello Fyne!")
	e := NewMyEntry(func(e *MyEntry) {
		s := e.Text
		e.SetText("")
		l.SetText("you type '" + s + "'.")
	})
	w.SetContent(
		// replaced(fyne v2): widget.Box -> container.NewH/VBox
		container.NewVBox(
			l, e,
		),
	)
	//a.Settings().SetTheme(theme.LightTheme())
	w.Resize(fyne.NewSize(300, 100))
	w.ShowAndRun()
}

```

▼リスト4-25 GUIアプリを作る: 電卓アプリ

```go
package main

import (
	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/layout"
	"fyne.io/fyne/v2/widget"
	"strconv"
)

type cdata struct {
	mem int    // 入力の前に記憶されている値
	cal string // 選択した演算キー
	flg bool   // 演算直後かどうか(演算直後:true/それ以外:false)
}

// 数字キーを生成
func createNumButtons(f func(v int)) *fyne.Container {
	// deprecated(fyne v2): fyne.NewContainerWithLayout -> container.New
	c := container.New(
		layout.NewGridLayout(3),
		widget.NewButton(strconv.Itoa(7), func() { f(7) }),
		widget.NewButton(strconv.Itoa(8), func() { f(8) }),
		widget.NewButton(strconv.Itoa(9), func() { f(9) }),
		widget.NewButton(strconv.Itoa(4), func() { f(4) }),
		widget.NewButton(strconv.Itoa(5), func() { f(5) }),
		widget.NewButton(strconv.Itoa(6), func() { f(6) }),
		widget.NewButton(strconv.Itoa(1), func() { f(1) }),
		widget.NewButton(strconv.Itoa(2), func() { f(2) }),
		widget.NewButton(strconv.Itoa(3), func() { f(3) }),
		widget.NewButton(strconv.Itoa(0), func() { f(0) }),
	)
	return c
}

// 演算キーを生成
func createCalcButtons(f func(c string)) *fyne.Container {
	// deprecated(fyne v2): fyne.NewContainerWithLayout -> container.New
	c := container.New(
		layout.NewGridLayout(1),
		widget.NewButton("CL", func() {
			f("CL")
		}),
		widget.NewButton("/", func() {
			f("/")
		}),
		widget.NewButton("*", func() {
			f("*")
		}),
		widget.NewButton("+", func() {
			f("+")
		}),
		widget.NewButton("-", func() {
			f("-")
		}),
	)
	return c
}

func main() {
	a := app.New()
	w := a.NewWindow("Calc")
	w.SetFixedSize(true)
	// 入力値
	l := widget.NewLabel("0")
	l.Alignment = fyne.TextAlignTrailing

	data := cdata{
		mem: 0,
		cal: "",
		flg: false,
	}
	// 演算キー選択時の計算処理
	calc := func(n int) {
		switch data.cal {
		case "":
			data.mem = n
		case "+":
			data.mem += n
		case "-":
			data.mem -= n
		case "*":
			data.mem *= n
		case "/":
			data.mem /= n
		}
		l.SetText(strconv.Itoa(data.mem))
		// 演算直後なのでflgをtrueにする
		data.flg = true
	}
	// 数字キー選択時の処理
	pushNum := func(v int) {
		s := l.Text
		if data.flg {
			// 演算直後に数字キーを選択した時、入力値をリセットする
			s = "0"
			data.flg = false
		}
		// 選択された数字を入力値の右に追加していく
		s += strconv.Itoa(v)
		n, err := strconv.Atoi(s)
		if err == nil {
			l.SetText(strconv.Itoa(n))
		}
	}
	// 演算キー選択時の処理
	pushCalc := func(c string) {
		if c == "CL" {
			// "CL"キーを選択した時、入力値と保持データをリセットする
			l.SetText("0")
			data.mem = 0
			data.flg = false
			data.cal = ""
			return
		}
		n, err := strconv.Atoi(l.Text)
		if err != nil {
			return
		}
		calc(n)
		data.cal = c
	}
	// "Enter"キー選択時の処理
	pushEnter := func() {
		n, err := strconv.Atoi(l.Text)
		if err != nil {
			return
		}
		calc(n)
		data.cal = ""
	}
	k := createNumButtons(pushNum)
	c := createCalcButtons(pushCalc)
	e := widget.NewButton("Enter", pushEnter)
	w.SetContent(
		// deprecated(fyne v2): fyne.NewContainerWithLayout -> container.New
		container.New(
			layout.NewBorderLayout(
				l, e, nil, c,
			),
			l, e, k, c,
		),
	)
	w.Resize(fyne.NewSize(300, 200))
	w.ShowAndRun()
}
```

▼リスト4-26 GUIアプリを作る: テキストエディタアプリ

```go
package main

import (
	"fyne.io/fyne/v2"
	"fyne.io/fyne/v2/app"
	"fyne.io/fyne/v2/container"
	"fyne.io/fyne/v2/dialog"
	"fyne.io/fyne/v2/layout"
	"fyne.io/fyne/v2/theme"
	"fyne.io/fyne/v2/widget"
	"os"
)

func main() {
	a := app.New()
	//a.Settings().SetTheme(theme.DarkTheme())
	w := a.NewWindow("Editor")
	edit := widget.NewEntry()
	edit.MultiLine = true
	// replaced(fyne v2): widget.ScrollContainer -> container.Scroll
	sc := container.NewScroll(edit)
	inf := widget.NewLabel("information bar.")
	// 新規ファイルの作成処理
	nf := func() {
		dialog.ShowConfirm("Alert", "Create New document?", func(f bool) {
			if f {
				edit.SetText("")
				inf.SetText("create new document.")
			}
		}, w)
	}
	// ファイルを開く処理
	of := func() {
		f := widget.NewEntry()
		dialog.ShowCustomConfirm("Open file name.", "OK", "Cancel",
			f, func(b bool) {
				if b {
					fn := f.Text + ".txt"
					// deprecated(go1.16): ioutil.ReadFile -> os.ReadFile
					ba, err := os.ReadFile(fn)
					if err != nil {
						dialog.ShowError(err, w)
					} else {
						edit.SetText(string(ba))
						inf.SetText("Open from file '" + fn + "'.")
					}
				}
			}, w)
	}
	// ファイルの保存処理
	sf := func() {
		f := widget.NewEntry()
		dialog.ShowCustomConfirm("Save file name.", "OK", "Cancel",
			f, func(b bool) {
				if b {
					fn := f.Text + ".txt"
					// deprecated(go1.16): ioutil.WriteFile -> os.WriteFile
					err := os.WriteFile(fn, []byte(edit.Text), os.ModePerm)
					if err != nil {
						dialog.ShowError(err, w)
						return
					}
					inf.SetText("Save to file '" + fn + "'.")
				}
			}, w)
	}
	// アプリの終了処理
	qf := func() {
		dialog.ShowConfirm("Alert", "Quit application?", func(f bool) {
			if f {
				a.Quit()
			}
		}, w)
	}
	tf := true
	// テーマの変更処理
	cf := func() {
		if tf {
			a.Settings().SetTheme(theme.LightTheme())
			inf.SetText("change to Light-Theme.")
		} else {
			a.Settings().SetTheme(theme.DarkTheme())
			inf.SetText("change to Dark-Theme.")
		}
		tf = !tf
	}
	// メニューバーを生成
	createMenubar := func() *fyne.MainMenu {
		return fyne.NewMainMenu(
			fyne.NewMenu("File",
				// ファイルの新規作成
				fyne.NewMenuItem("New", func() {
					nf()
				}),
				// ファイルを開く
				fyne.NewMenuItem("Open...", func() {
					of()
				}),
				// ファイルの保存
				fyne.NewMenuItem("Save...", func() {
					sf()
				}),
				// テーマの変更
				fyne.NewMenuItem("Change Theme", func() {
					cf()
				}),
				// アプリの終了
				fyne.NewMenuItem("Quit", func() {
					qf()
				}),
			),
			fyne.NewMenu("Edit",
				// テキストのカット
				fyne.NewMenuItem("Cut", func() {
					edit.TypedShortcut(&fyne.ShortcutCut{
						Clipboard: w.Clipboard()})
					inf.SetText("Cut text.")
				}),
				// テキストのコピー
				fyne.NewMenuItem("Copy", func() {
					edit.TypedShortcut(&fyne.ShortcutCopy{
						Clipboard: w.Clipboard()})
					inf.SetText("Copy text.")
				}),
				// テキストのペースト
				fyne.NewMenuItem("Paste", func() {
					edit.TypedShortcut(&fyne.ShortcutPaste{
						Clipboard: w.Clipboard()})
					inf.SetText("Paste text.")
				}),
			),
		)
	}
	// ツールバーを生成
	createToolbar := func() *widget.Toolbar {
		return widget.NewToolbar(
			// ファイルの新規作成
			widget.NewToolbarAction(theme.DocumentCreateIcon(), func() {
				nf()
			}),
			// ファイルを開く
			widget.NewToolbarAction(theme.FolderOpenIcon(), func() {
				of()
			}),
			// ファイルの保存
			widget.NewToolbarAction(theme.DocumentSaveIcon(), func() {
				sf()
			}),
		)
	}
	mb := createMenubar()
	tb := createToolbar()
	w.SetMainMenu(mb)
	w.SetContent(
		// deprecated(fyne v2): fyne.NewContainerWithLayout -> container.New
		container.New(
			layout.NewBorderLayout(
				tb, inf, nil, nil,
			),
			tb, inf, sc,
		),
	)
	w.Resize(fyne.NewSize(500, 500))
	w.ShowAndRun()
}
```