# ymst
---

### 今日やること

 - iOSアプリ開発。個人開発のアプリでSwiftUIを調べながら作っています。
    1. メニューからメインのタブ画面の各タブを開く
    2. testflightにアップロード
    3. ログイン機能

---

### 結果

 - iOSアプリ開発。個人開発のアプリでSwiftUIを調べながら作っています。
    1. メニューからメインのタブ画面の各タブを開く ->未達
    2. testflightにアップロード -> 手付かず
    3. ログイン機能　-> 手付かず

    😢😢😢
---

#### 1. メニューからメインのタブ画面の各タブを開く🤔

- ![image](https://raw.githubusercontent.com/yymsht/myslide/master/assets/img/test.jpg)

---
### Yattakoto
- メニューからメインのタブ画面の各タブを開く
    - 環境変数みたいなので`@Environment(\.selectedTab) var canselIndex: Int`で渡そうとしたけどダメだった->タブ画面とメニュー画面の環境（ViewController?）が違うから?🤔
    - メインタブ画面に`@State`で状態管理（どのタブ）プロパティを持って、各タブの下層の画面からメニューを開く時に、メニューにそのプロパティをわたし、メニューでそれを変更（力技💪）
        - メインタブ画面に`@State var selectedIndex`
        - タブ内の下層画面の各VMをinitするときの引数に `selectedIndex: Binding<Int>`
        - 各タブ下層画面のViewに`let currentTab: Int = N`を入れる
        - 各子featureごとのNavigatorを削除、Viewに実装
        - BaseViewModelのプロパティのNavigatorを削除
        - BaseViewのsetNavigatorを削除
        - VMでNavigatorをよんでいたメソッド`toMenu()`みたいなのを削除
        - VMのプロパティのNavigatorを削除
    - testflightにアップロード
    - ログイン機能

---
### Wakattakoto

- Swift5.1のProperty Wrappersは`@Environment`とか`@Binding`とか色々あるけど、全部がラップしてるプロパティの値の変化を通知するものではない。
- `@Environment`は環境というスコープで静的な変数としてつかえる感じで便利だけど、環境(たぶんviewController???)が異なると別の値になる。それだとAndroidで普通にActivityのプロパティをFragmentで使い回す感じ？　->もっとすごいものかもしれないので引き続き調べます。
- `@State`は便利。ビューの状態管理のプロパティに使うとこの値をViewModelや他のViewが変更した時にそのままビューの中の`if isHoge {表示 }else{非表示}`みたいなところに通知し、ビューの変更を行ってくれる。
---
### Tsugiyarukoto
- メニュー画面でタブを操作する実装に関しては絶対にもっとスマートなやり方があるはずなので、ある画面の状態を別の画面から操作するようなデータのやりとりのパターンを色々と勉強していきたい。
- ↑そもそもiOSの画面のライフサイクルとかを理解していないのでそもそも画面描画の処理とかをまとめてあるブログとかもどうにか読みたい。
