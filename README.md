# 等焦部分多様体シミュレータ / Equifocal Submanifold Demos

対称空間内の**等焦部分多様体**（equifocal submanifold）と，ユークリッド空間内の**等径部分多様体**（isoparametric submanifold）を，平坦切断 $\Sigma$ 上の**焦超平面配置**として可視化するデモ集です．外部ライブラリ・ビルド・サーバを一切必要とせず，各デモは**単一の HTML ファイル**だけで動作します（描画は HTML Canvas 2D API）．

> Interactive, dependency-free demos for equifocal and isoparametric submanifolds — each one a single self-contained HTML file.

## ▶ ライブデモ

**デモ一覧:** https://nagajin.github.io/equifocal-demos/

| デモ | 内容 | リンク |
|---|---|---|
| 切断と焦超平面配置 | 焦超平面配置・Weyl 軌道・焦半径・平行写像の退化 | [section-arrangement.html](https://nagajin.github.io/equifocal-demos/section-arrangement.html) |

## 設計の中心にある考え方

等焦部分多様体 $M \subset N$ の幾何は，周囲次元がどれだけ大きくても，**平坦切断 $\Sigma$ 上の焦超平面配置（＋重複度）**に完全に符号化されます．したがって階数 $r = \operatorname{codim} M \le 2$ なら，2 次元の絵 1 枚で $M$ の主曲率・焦半径・平行族・焦部分多様体の次元がすべて読めます．本デモはこの「設計図」を対話的に操作するものです．

制限ルート系 $\Delta$ と重複度 $m_\alpha$ を与えると，周囲空間の型に応じて次が定まります．

| 型 | 焦超平面 | 主曲率 $A_\xi\vert_{\mathfrak p_\alpha}$ | $W$ |
|---|---|---|---|
| ユークリッド型（$s$-表現の主軌道＝等径部分多様体） | $\alpha(x)=0$ | $-\alpha(\xi)/\alpha(x)$ | 有限 Coxeter 群 |
| コンパクト型（対称空間の等焦部分多様体） | $\alpha(x)\in\pi\mathbb{Z}$ | $-\alpha(\xi)\cot\alpha(x)$ | アフィン Weyl 群 |

- $\dim M = \sum_{\alpha\in\Delta^+} m_\alpha$, $\dim N = \dim M + r$
- **焦半径** $t$ ⟺ 半直線 $q+t\xi$ が焦超平面に乗る
- $\dim\ker d(F^\xi_t)_q = \sum m_\alpha$（その $t$ で当たる超平面の総和）＝ 焦部分多様体での次元降下
- $M\cap\Sigma = W\cdot q$（$q$ は正則点）

**平坦切断の仮定について**：一般には強 $M$–ヤコビ場の零点（$\ker dF^\xi_t$ が測る接方向焦点）と通常の焦点は一致しません．両者が一致するのは**切断が平坦**なときで，等焦部分多様体はこれを満たします．本デモは一貫して $\ker dF^\xi_t$ で焦点を測っています．

## 収録デモ

### 切断と焦超平面配置 (`section-arrangement.html`)

- **ルート系**：$A_1$, $BC_1$（階数 1），$A_1\times A_1$, $A_2$, $B_2(=C_2)$, $BC_2$, $G_2$（階数 2）．非簡約型 $BC$ を含むので，コンパクト型では $\alpha$ と $2\alpha$ が超平面を半間隔に二重化する様子が見えます．
- **プリセット 25 件**：$S^5$, $\mathbb{C}P^3$, $\mathbb{H}P^2$, $\mathbb{O}P^2$, $S^2\times S^2$, $SU(3)/SO(3)$, $SU(3)$, $SU(6)/Sp(3)$, $E_6/F_4$, $\tilde G_2(\mathbb{R}^5)$, $Sp(2)$, $G_2(\mathbb{C}^6)$, $G_2(\mathbb{H}^6)$, $G_2/SO(4)$, $G_2$，および Cartan の等径超曲面 $M^3\subset S^4$ ほか．各プリセットで $\dim N = \sum m_\alpha + r$ が既知次元と一致するかを画面上で検証します．
- **操作**：$q$ と $\xi$ をドラッグ，$t$ スライダと再生で平行写像 $F^\xi_t$ をアニメーション，焦半径表の行クリックでその $t$ へジャンプ，ホイールでズーム．
- **表示**：Weyl 軌道 $W\cdot q$，アルコーブ（Weyl 部屋），曲率法線 $n_\alpha$，平行部分多様体 $W\cdot(q+t\xi)$，球面切断（ユークリッド型・$r=2$），閉測地線としての切断（$r=1$）．

#### 球面内の等径超曲面としての読み方

ユークリッド型・$r=2$ で原点中心の球面と交わると，球面内の等径超曲面が得られます．相異なる主曲率の個数 $g$ は焦超平面の本数に，Münzner の $m_i = m_{i+2}$ は配置上の重複度の交代性に対応します．階数 2 の結晶群的 Coxeter 配置が $g\in\{1,2,3,4,6\}$ を与えることと美しく呼応します．

例：$A_2$・$m=1$ を選ぶと，大円上に焦点 6 個と $M\cap\Sigma$ の 6 点が交互に並ぶ Cartan の等径超曲面 $M^3\subset S^4$ の絵になります．

## 数値的な整合性チェック

実装は次の関係が厳密に成り立つことを確認しています．

- 全 25 プリセットで $\dim N = \sum_{\alpha\in\Delta^+} m_\alpha + r$ が独立に知られた次元と一致
- ユークリッド型で 焦半径 $= 1/\lambda$（Terng）
- $BC_2$ ユークリッド型（$G_2(\mathbb{C}^6)$，$m=(4,2,1)$）で $e_i$ と $2e_i$ が同一直線に合流し，重複度が $(5,2,5,2)$ と交代
- $BC_1$ コンパクト型（$\mathbb{C}P^3$，$m_\alpha=4$, $m_{2\alpha}=1$）で焦点が $\pi/2$ 間隔・重複度 $5,1$ の交代 → 焦部分多様体は 1 点（次元降下 5）と $\mathbb{C}P^2$（次元降下 1）
- 同じく $\mathbb{C}P^3$，$q$ が半径 $\pi/4$ の測地超球面のとき主曲率は $-\cot(\pi/4)=-1$（重複度 4）と $-2\cot(\pi/2)=0$（重複度 1）

## 符号規約

- 形状作用素は $A_\xi X = -\nabla_X\xi$（$\xi$ は平行法ベクトル場）．
- コンパクト型の切断は長さ $2\pi$ の閉測地線を単位に正規化（短根 $|\alpha|=1$）．

## 参考文献

- C.-L. Terng, *Isoparametric submanifolds and their Coxeter groups*, J. Differential Geom. **21** (1985), 79–107.
- C.-L. Terng and G. Thorbergsson, *Submanifold geometry in symmetric spaces*, J. Differential Geom. **42** (1995), 665–718.
- E. Heintze, R. S. Palais, C.-L. Terng and G. Thorbergsson, *Hyperpolar actions on symmetric spaces*, in Geometry, Topology & Physics, Int. Press, 1995, 214–245.
- N. Koike, *Complex equifocal submanifolds and infinite-dimensional anti-Kaehlerian isoparametric submanifolds*, Tokyo J. Math. **28** (2005), 201–247.
- H. F. Münzner, *Isoparametrische Hyperflächen in Sphären*, Math. Ann. **251** (1980), 57–71.

## ライセンス

MIT License © 2026 長塚 悠仁 (Yuto Nagatsuka)
