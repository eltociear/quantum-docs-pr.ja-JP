# <a name="articles"></a><span data-ttu-id="642aa-101">記事</span><span class="sxs-lookup"><span data-stu-id="642aa-101">Articles</span></span>

<span data-ttu-id="642aa-102">このディレクトリには、Quantum 開発キットのドキュメントの記事があります。</span><span class="sxs-lookup"><span data-stu-id="642aa-102">In this directory you can find the articles for the documentation of the Quantum Development Kit.</span></span> <span data-ttu-id="642aa-103">このディレクトリには次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="642aa-103">This directory contains:</span></span>

- <span data-ttu-id="642aa-104">**記事のディレクトリ**: ドキュメントの各セクションの記事が含まれています。</span><span class="sxs-lookup"><span data-stu-id="642aa-104">**Articles directories**: contain the articles for each section of the documentation.</span></span> <span data-ttu-id="642aa-105">これらのディレクトリには、次の内容が表示されます。</span><span class="sxs-lookup"><span data-stu-id="642aa-105">In these directories you can find the following contents:</span></span>
  
  - <span data-ttu-id="642aa-106">すべてのディレクトリには、 `toc.yml` メインの目次 (TOC) にディレクトリの内容を表示するファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="642aa-106">Every directory contains a `toc.yml` file to display the content of the directory in the main Table Of Contents (TOC).</span></span>
  - <span data-ttu-id="642aa-107">ドキュメントを含む記事を Markdown します。</span><span class="sxs-lookup"><span data-stu-id="642aa-107">Markdown articles that contain the documentation.</span></span> <span data-ttu-id="642aa-108">これらの記事は、 [Microsoft Docs 共同作成者ガイド](https://docs.microsoft.com/en-us/contribute/)のガイドラインに従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="642aa-108">These articles should follow the guidelines of the [Microsoft Docs contributor guide](https://docs.microsoft.com/en-us/contribute/).</span></span>
  - <span data-ttu-id="642aa-109">記事サブディレクトリ。</span><span class="sxs-lookup"><span data-stu-id="642aa-109">Articles sub-directories.</span></span> <span data-ttu-id="642aa-110">これらのサブディレクトリにも、独自のファイルが含まれている必要があり `toc.yml` ます。</span><span class="sxs-lookup"><span data-stu-id="642aa-110">These sub-directories should also contain their own `toc.yml` file.</span></span>

> <span data-ttu-id="642aa-111">:p encil: 親ファイル内のファイルを直接参照することはできますが `*.md` `TOC.yml` 、順序を維持するために、現在のディレクトリのからのみ参照することをお勧めし `toc.yml` ます。</span><span class="sxs-lookup"><span data-stu-id="642aa-111">:pencil: Although it's possible to refer the `*.md` files directly in the parent `TOC.yml` file, to keep things ordered we only refer them from the `toc.yml` of their current directory.</span></span>

- <span data-ttu-id="642aa-112">目次 **(目次) `TOC.yml` ファイル**: このファイルでは、WEB サイトの toc セクションが、 `toc.yml` 各セクションのディレクトリのメインファイルへの参照と共に一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="642aa-112">**Main table of contents (TOC) `TOC.yml` file**: in this file the sections of the website TOC are listed together with the reference to the main `toc.yml` file of the directory of each section.</span></span>
- <span data-ttu-id="642aa-113">**`index.yml`** ドキュメントのランディングページの構成を使用した YAML。</span><span class="sxs-lookup"><span data-stu-id="642aa-113">**`index.yml`** YAML with the configuration of the landing page of the documentation.</span></span>
- <span data-ttu-id="642aa-114">**`\media`**: ドキュメントに使用されているすべてのイメージを格納するディレクトリ。</span><span class="sxs-lookup"><span data-stu-id="642aa-114">**`\media`**: A directory to store all the images used in the documentation.</span></span> <span data-ttu-id="642aa-115">これには、 `\media\src` イメージのソースファイルを格納するためのサブディレクトリが含まれています。</span><span class="sxs-lookup"><span data-stu-id="642aa-115">It contains a `\media\src` subdirectory to store source files of the images.</span></span>
- <span data-ttu-id="642aa-116">**ライセンスファイル**: 法的ライセンスを含むファイル</span><span class="sxs-lookup"><span data-stu-id="642aa-116">**License files**: files containing legal licenses</span></span>
- <span data-ttu-id="642aa-117">**テクニカルファイル**: マクロおよびメタデータを含むファイル。</span><span class="sxs-lookup"><span data-stu-id="642aa-117">**Technical files**: files containing macros and metadata.</span></span>

## <a name="guidelines"></a><span data-ttu-id="642aa-118">ガイドライン</span><span class="sxs-lookup"><span data-stu-id="642aa-118">Guidelines</span></span>

<span data-ttu-id="642aa-119">このディレクトリの共同作成者向けの組織に関する一般的なガイドラインを次に示します。</span><span class="sxs-lookup"><span data-stu-id="642aa-119">Some general guidelines about the organization of this directory for contributors:</span></span>

- <span data-ttu-id="642aa-120">すべてのディレクトリまたはサブディレクトリには、 `toc.yml` 同じレベルのアーティクルまたは `toc.yml` その子ディレクトリのファイルを参照する独自のファイルが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="642aa-120">Every directory or sub-directory should contain its own `toc.yml` file in which are referred the same-level articles or the `toc.yml` files of its child directories.</span></span>
- <span data-ttu-id="642aa-121">リポジトリのディレクトリの編成は、ドキュメント web サイトの目次の編成にできるだけ近いものにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="642aa-121">The organization of the directories of the repository should be as close as possible to the organization of the table of contents of the documentation website.</span></span>
- <span data-ttu-id="642aa-122">すべてのイメージはに格納され、[アーティクル] フォルダーには保存され `articles\media` ません。</span><span class="sxs-lookup"><span data-stu-id="642aa-122">All the images should be stored in `articles\media` and not in the articles folder.</span></span>
- <span data-ttu-id="642aa-123">記事のタイトル、TOC 内の名前、およびメタデータの*uid*は、Markdown ドキュメントの H1 ヘッダーを明確に表したものとして、可能な限り近くに配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="642aa-123">The titles of the articles, the names in the TOC and the *uid* of the metadata should be as close as possible among them and represent clearly the H1 header of the Markdown document.</span></span>

## <a name="adding-images"></a><span data-ttu-id="642aa-124">追加 (イメージを)</span><span class="sxs-lookup"><span data-stu-id="642aa-124">Adding images</span></span>

<span data-ttu-id="642aa-125">画像がダークモードで正しく表示されるようにするには、ohp シートを使用しないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="642aa-125">To have the images rendering properly in dark mode you must avoid transparencies.</span></span>
- <span data-ttu-id="642aa-126">ファイルの場合 `*.jpg` 、ファイル形式は透過的な要素をサポートしていないため、何もする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="642aa-126">For `*.jpg` files you don't need to do anything since the file format doesn't support transparent elements.</span></span>
- <span data-ttu-id="642aa-127">ファイルの場合 `*.png` は、白の背景を追加するか、アルファチャネルの値を100に変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="642aa-127">For `*.png` files you must add a white background or change the value of the alpha channel to 100.</span></span> <span data-ttu-id="642aa-128">Windows でこれを行う最も簡単な方法は、ファイルをペイントで開いて保存し、元のファイルを上書きすることです。</span><span class="sxs-lookup"><span data-stu-id="642aa-128">The easiest way to do this in Windows is by opening the file in Paint and saving, overwriting the original file.</span></span>
- <span data-ttu-id="642aa-129">ファイルの場合は `*.svg` 、最も低いレイヤーに白い四角形を追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="642aa-129">For `*.svg` files you must add a white rectangle in the lowest layer.</span></span> <span data-ttu-id="642aa-130">これを行うには、Inkscape を使用します。</span><span class="sxs-lookup"><span data-stu-id="642aa-130">You can do this with Inkscape:</span></span>
  - <span data-ttu-id="642aa-131">`*.svg` ファイルを開きます。</span><span class="sxs-lookup"><span data-stu-id="642aa-131">Open the `*.svg` file.</span></span>
  - <span data-ttu-id="642aa-132">四角形メーカーツールを選択し、元の図の上に白い四角形を描画します。</span><span class="sxs-lookup"><span data-stu-id="642aa-132">Select the square maker tool and draw a white rectangle on top of the original figure.</span></span>
  - <span data-ttu-id="642aa-133">[オブジェクトの選択と変換] ツールを選択するには、黒い矢印をクリックするか、F1 キーを押します。</span><span class="sxs-lookup"><span data-stu-id="642aa-133">Select the tool "Select and transform objects" by clicking in the dark arrow or pressing F1.</span></span>
  - <span data-ttu-id="642aa-134">四角形が選択されている状態で、ツールバー要素内をクリックして [下まで選択] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="642aa-134">While having the rectangle selected, click in the toolbar element "Lower selection to bottom (End)".</span></span>
  - <span data-ttu-id="642aa-135">マウスまたは方向キーを使用して四角形を調整します。</span><span class="sxs-lookup"><span data-stu-id="642aa-135">Adjust the rectangle with the mouse or the arrow keys.</span></span>