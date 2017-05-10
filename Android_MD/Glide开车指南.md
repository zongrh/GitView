
###1、基本使用
**添加Glide到你的设置中**
首先，添加Glide到你的工程依赖里，截止本文写作时，最新的Glide版本是3.7.0.

**Gradle**和大多数依赖库一样，在Gradle项目中只需要在build.gradle中添加一行：

    compile 'com.github.bumptech.glide:glide:3.7.0'

**Maven**  Glide也支持 Maven项目:

    <dependency>
    <groupId>com.github.bumptech.glide</groupId>
    <artifactId>glide</artifactId>
    <version>3.7.0</version>
    <type>aar</type>
    </dependency>

#####第一次尝试：从一个 URL加载图片

和Picasso一样，Glide使用一个流接口（Fluent Interface）。用Glide完成一个完整的图片加载功能请求，需要向其构造器中至少传入3个参数，分别是：

- with(Context context)- Context是许多Android API需要调用的， Glide也不例外。这里Glide非常方便，你可以任意传递一个Activity或者Fragment对象，它都可以自动提取出上下文。

- load(String imageUrl) - 这里传入的是你要加载的图片的URL，大多数情况下这个String类型的变量会链接到一个网络图片。

- into(ImageView targetImageView) - 将你所希望解析的图片传递给所要显示的ImageView。
理论上的解释通常难以掌握，让我们随手举个栗子：

        ImageView targetImageView = (ImageView) findViewById(R.id.imageView);
        String internetUrl = "http://i.imgur.com/DvpvklR.png";

        Glide
        .with(context)
        .load(internetUrl)
        .into(targetImageView);

就上面这几行！如果这个URL链接的图片的确存在，并且你的ImageView可见，你将会在1~2秒见到这张图片被加载。假如这张图片不存在，Glide会回调相应的出错接口（这个以后再具体介绍）。 你可能已经被这个3行代码说服，觉得这个Glide的确对你有用。不过，现在你所见到的，只是Glide全部特性里的冰山一角而已。

###2、高级加载
#####从Res资源中加载

首先介绍从Android资源中加载。不同于上一节的String类型的网络URL，这里是一个Int型的的资源id。

    int resourceId = R.mipmap.ic_launcher;

    Glide
    .with(context)
    .load(resourceId)
    .into(imageViewResource);
如果你觉得R.mipmap.没见过, 这是Android的一个处理图标的新方法。
虽然，你可以直接在ImageView的属性里添加这一资源。但是，如果你使用Glide这种更高级的方式进行动态转换，你的应用可以做得非常有趣。
#####从文件中加载

从资源文件加载，通常是固定的，当你让用户任意选择一张图片来显示的时候，这个文件的路径并非是开发人员预先设定的，从图片文件中加载对于实际应用将会非常有用。需要传递的参数也仅仅是一个文件对象，举个栗子：

    // this file probably does not exist on your device. However, you can use any file path, which points to an image file

    File file = new File(Environment.getExternalStoragePublicDirectory(Environment.DIRECTORY_PICTURES), "Running.jpg");

    Glide
    .with(context)
    .load(file)
    .into(imageViewFile);

#####从Uri加载

最后介绍从Uri中加载图片，这里的请求跟上面的方法并无太大差异，直接看代码：

    // 这个可以是任何Uri. 这里为了演示，我们只创建了一个指向桌面图标的Uri

    Uri uri = resourceIdToUri(context, R.mipmap.future_studio_launcher);

    Glide
    .with(context)
    .load(uri)
    .into(imageViewUri);

下面一个小的工具函数可以将资源id转换为一个Uri：

    public static final String ANDROID_RESOURCE = "android.resource://";
    public static final String FOREWARD_SLASH = "/";

    private static Uri resourceIdToUri(Context context, int resourceId) {
    return Uri.parse(ANDROID_RESOURCE + context.getPackageName() + FOREWARD_SLASH + resourceId);
    }
当然，Uri并不一定是从资源id中创建，它可以是任意Uri。
###3、Glide — 适配器 (ListView, GridView)
#####相册展示: ListView

第一步，我们需要准备些测试图片。我们从eatfoody.com网站获取一些美食图片链接imgur

    public static String[] eatFoodyImages = {
        "http://i.imgur.com/rFLNqWI.jpg",
        "http://i.imgur.com/C9pBVt7.jpg",
        "http://i.imgur.com/rT5vXE1.jpg",
        "http://i.imgur.com/aIy5R2k.jpg",
        "http://i.imgur.com/MoJs9pT.jpg",
        "http://i.imgur.com/S963yEM.jpg",
        "http://i.imgur.com/rLR2cyc.jpg",
        "http://i.imgur.com/SEPdUIx.jpg",
        "http://i.imgur.com/aC9OjaM.jpg",
        "http://i.imgur.com/76Jfv9b.jpg",
        "http://i.imgur.com/fUX7EIB.jpg",
        "http://i.imgur.com/syELajx.jpg",
        "http://i.imgur.com/COzBnru.jpg",
        "http://i.imgur.com/Z3QjilA.jpg",
    };
第二步，我们需要一个activity创建一个adapter，并绑定到一个ListView上：

    public class UsageExampleAdapter extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        setContentView(R.layout.activity_usage_example_adapter);

        listView.setAdapter(new ImageListAdapter(UsageExampleAdapter.this, eatFoodyImages));
    }
    }
第三步，一起看一下adapter的layout文件，非常简单：

    <?xml version="1.0" encoding="utf-8"?>
    <ImageView xmlns:android="http://schemas.android.com/apk/res/android"
       android:layout_width="match_parent"
       android:layout_height="200dp"/>
这个xml文件里的配置会影响到列表里的每个图片，所有图片的高度都设置为200dp，宽度适配设备的宽度。虽然上面的配置显示出的图片不是很优美，但这不是本文的重点关注的内容。

在我们看到结果之前，我们需要为这个ListView实现这个adapter。让我们的美食图片绑定到适配器，每一栏显示一张图片。
    public class ImageListAdapter extends ArrayAdapter {
    private Context context;
    private LayoutInflater inflater;

    private String[] imageUrls;

    public ImageListAdapter(Context context, String[] imageUrls) {
        super(context, R.layout.listview_item_image, imageUrls);

        this.context = context;
        this.imageUrls = imageUrls;

        inflater = LayoutInflater.from(context);
    }

    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        if (null == convertView) {
            convertView = inflater.inflate(R.layout.listview_item_image, parent, false);
        }

        Glide
            .with(context)
            .load(imageUrls[position])
            .into((ImageView) convertView);

        return convertView;
    }
    }

在ImageListView的getView（）方法里，你会惊奇地发现Glide的调用是跟之前介绍的常规加载方法一致，不管在什么样子的app中使用Glide，使用Glide的方式都是一样的。

作为一个资深的Android开发者，你应当知道如何在ListView复用layout，来让滑动操作更加快速流畅。你不用担心滑动过程中的一些其他问题，Glide可以自动地处理请求的取消、ImageView的回收，并且加载正确的图片到对应的ImageView里。

**Glide的强项: 缓存**

当你不断向上向下滑动多次后，你会发现图片会比之前加载地更快。在新手机上，可能需要稍微多等一会。你可以很容易想到，这些图片由于被缓存到磁盘上，用的时候不必再从网络获取。Glide的缓存实现是基于Picasso的一个方法，让你可以更简单地使用。具体可以缓存的大小取决于设备磁盘的大小。

当加载一张图片时，Glide使用这些资源：内存、磁盘和网络（根据由快到慢）。第二次加载的时候，你啥都不用做，一旦Glide智能地创建了合适大小的图片缓存，将为你分担了所有复杂工作。我们会在随后的文章中进一步学习缓存。

#####简单的图库应用: GridView

GridView加载图片的使用跟ListView加载没有任何区别，你可以使用一样的adapter，只要切换Activity的布局到GridView：

    <?xml version="1.0" encoding="utf-8"?>
    <GridView
    android:id="@+id/usage_example_gridview"
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:numColumns="2"/>

**其他应用: 当ImageVIew是一个子控件**

目前为止，我们只介绍了整个adapter内只有一个ImageView。当ImageView只是adapter内很多控件中的一小部分控件时，这个方法依然适用。只是你的getView()代码可能有些许不一样，但用Glide加载都是一样的方式。

###4、位图& 淡入淡出动画
我们根本没有必要讨论或解释：空白的ImageView在任何UI中看起来都是丑陋的。如果你在使用Glide，你很可能正在从网络上加载图片。假如你网络的环境不好，加载过程可能需要花费大量的时间。这时候就需要一个占位图先显示出来，直到实际的图片加载并处理完毕。

Glide的流接口让这个工作变得很简单！只要调用.placeHolder() ，并传递进去一个图片资源，Glide会显示那个占位图，直到实际图片准备完毕。

    Glide
    .with(context)
    .load(UsageExampleListViewAdapter.eatFoodyImages[0])
    .placeholder(R.mipmap.ic_launcher) // can also be a drawable
    .into(imageViewPlaceholder);
显然，你不能设置一个网络的url当作占位图。假如那样，占位图也需要时间去下载。App内的资源和图片毫无疑问是可以使用的。同时，由于Glide的load()可以接受各式的参数，这些参数可能是不能加载的（无网络连接，服务器挂了，等等），被删除的或者其他无法访问的。在下一节，我们会介绍出错占位图。

**出错占位图: .error()**

我们假设我们的app尝试从网页加载一张图片，但网页不可访问，Glide会给我们选项去进行出错的回调，并采取合适的行动。（选项问题以后再讨论，目前来说还是比较复杂的）。在大多数情况下，占位图可以完全足够用来表明图片无法加载。

跟之前栗子中预加载的占位图一样，调用Glide的流接口即可，只是有命名上有点不一样，叫error()：

    Glide
    .with(context)
    .load("http://futurestud.io/non_existing_image.png")
    .placeholder(R.mipmap.ic_launcher) // can also be a drawable
    .error(R.mipmap.future_studio_launcher) // will be displayed if the image cannot be loaded
    .into(imageViewError);
上面的代码中，如果从load()里传入的图片无法被加载，Glide会显示R.mipmap.future_studio_launcher来代替。再次强调一下，error()可以接受的只能是已经被初始化的图片资源或者指向图片资源的id(R.drawable.<drawable-keyword>)。

**crossFade()的使用**

无论你是否使用占位图，对于UI来说，图片的改变是相当大的一个动作。一个简单的方法可以让这个变化更平滑，更让人眼接受，这就是使用crossfade动画。Glide支持标准的crossfade动画，（对于目前版本3.6.1）是默认可用的。如果你想要使用crossfade动画，你只要在在构造器里添加另外一个调用：

    Glide
    .with(context)
    .load(UsageExampleListViewAdapter.eatFoodyImages[0])
    .placeholder(R.mipmap.ic_launcher) // can also be a drawable
    .error(R.mipmap.future_studio_launcher) // will be displayed if the image cannot be loaded
    .crossFade()
    .into(imageViewFade);
crossFade()方法有另外一个特征：.crossFade(int duration),如果你想要减慢（或加快）动画，随便传入一个毫秒级的时间进去感受一下。默认的动画时间是300毫秒。

**dontAnimate()的使用**

如果你只是直接显示图片，而不需要crossfade效果，那就在Glide的请求构造里调用.dontAnimate()：

    Glide
    .with(context)
    .load(UsageExampleListViewAdapter.eatFoodyImages[0])
    .placeholder(R.mipmap.ic_launcher) // can also be a drawable
    .error(R.mipmap.future_studio_launcher) // will be displayed if   the image cannot be loaded
    .dontAnimate()
    .into(imageViewFade);
你会直接看到图片，没有渐入的过程。请你确认你有自己的理由要这么做。

提醒你个很重要的事，这些参数都是独立的，并且设置不依赖彼此。例如，你可以只设置.error()，而不用调用.placeholder()。你可以设置crossFade()动画，而不用设置占位图。参数的任意结合都是可行的。

###5、图片大小 & 缩放
**resize(x, y)调整图片大小**

理想情况下，你的服务器或者API能够返回给你恰好所需分辨率的图片，这是在网络带宽、内存消耗和图片质量下的完美方案。

跟Picasso比起来，Glide在内存上占用更优化。Glide在缓存和内存里自动限制图片的大小去适配ImageView的尺寸。Picasso也有同样的能力，但需要调用fit()方法。用Glide时，如果图片不需要自动适配ImageView，调用override(horizontalSize, verticalSize)，它会在将图片显示在ImageView之前调整图片的大小。

    Glide
    .with(context)
    .load(UsageExampleListViewAdapter.eatFoodyImages[0])
    .override(600, 200) // resizes the image to these dimensions (in pixel). does not respect aspect ratio
    .into(imageViewResize);
这个设置可能也是有利于没有明确目标，但已知尺寸的视图上。例如，如果app想要预先缓存在splash屏幕上，还没法测量出ImageVIews具体宽高。但，如果你已经知道图片应当为多大，使用override可以提供一个指定的大小的图片。

**缩放图片**

现在，对于任何图像的任何处理，调整图像的大小可能会扭曲长宽比，丑化图片的显示。在大多数情况下，你希望防止这种事情发升。Glide提供了变换去处理图片显示，通过设置centerCrop 和 fitCenter，可以得到两个不同的效果。

**CenterCrop**

CenterCrop()会缩放图片让图片充满整个ImageView的边框，然后裁掉超出的部分。ImageVIew会被完全填充满，但是图片可能不能完全显示出。

    Glide
    .with(context)
    .load(UsageExampleListViewAdapter.eatFoodyImages[0])
    .override(600, 200) // resizes the image to these dimensions (in pixel)
    .centerCrop() // this cropping technique scales the image so that it fills the requested bounds and then crops the extra.
    .into(imageViewResizeCenterCrop);

**FitCenter**

fitCenter()会缩放图片让两边都相等或小于ImageView的所需求的边框。图片会被完整显示，可能不能完全填充整个ImageView。

    Glide
    .with(context)
    .load(UsageExampleListViewAdapter.eatFoodyImages[0])
    .override(600, 200)
    .fitCenter() 
    .into(imageViewResizeFitCenter);
我们会在随后的文章中介绍除了centerCrop() 和 fitCenter()以外的自定义变换方法。

###6、缓存基础
**缓存基础**

Android应用中一个较好的图片的处理加载，会最小化网络请求的消耗。Glide也是一样，默认使用内存和磁盘缓存来避免不必要的网络请求。我们将在后续的文章中详细介绍这些细节。如果你等不及，可以去浏览一下关于这个主题的官方文档。

目前，重要的处理方式是所有的图片请求都会被缓存在内存和磁盘上。大多数情况下，缓存是一个非常有用的东西，但在一些特殊的情况下并不是很明智。在下一节中，我们会介绍如何为单独的请求调整Glide的缓存方式。

**使用缓存的策略**

如果你在前面用Glide用的很溜，你可能注意到你并不需要额外自己激活缓存。Glide本身自带缓存。然而，如果你的图片变化的非常快，你需要避免一些缓存。

Glide提供了一些方法去避免内存缓存和磁盘缓存。我们先看看内存缓存。

**内存缓存**

我们通过一个非常简单的请求：从网络加载一个图片到ImageView：

    Glide  
    .with( context )
    .load( eatFoodyImages[0] )
    .skipMemoryCache( true )
    .into( imageViewInternet );
你已经注意到我们调用了.skipMemoryCache( true )去特意告诉Glide跳过内存缓存。这意味着Glide不会把这个图片缓存到内存里。重要是，这个只影响内存缓存！Glide为了避免以后的网络请求，仍然会缓存到磁盘。

由于Glide默认会将所有的图片资源缓存到内存中，因此，没有必要手动调用.skipMemoryCache( false )了。

提示：注意到现实情况，如果你要对同一个URL做一个初始化的请求，第一次没使用.skipMemoryCache( true )，然后第二次使用了，将会获取缓存在内存中的资源。当你调整缓存行为的时候，确保请求的都是指向同一个资源，

**跳过磁盘缓存**

如上面所讲到的，即使你关闭了内存缓存，所请求的图片仍然会被保存在设备的磁盘存储上。如果你有一张不段变化的图片，但是都是用的同一个URL，你可能需要禁止磁盘缓存了。

你可以用.diskCacheStrategy()方法改变Glide的行为。不同于.skipMemoryCache()方法，它将需要从枚举型变量中选择一个，而不是一个简单的boolean。如果你想要禁止请求的磁盘缓存，使用枚举型变量DiskCacheStrategy.NONE作为参数。

    Glide  
    .with( context )
    .load( eatFoodyImages[0] )
    .diskCacheStrategy( DiskCacheStrategy.NONE )
    .into( imageViewInternet );
上面代码里的图片根本不会被保存在磁盘上。然后，默认情况下它仍然使用内存缓存！为了同时禁止掉两个缓存，结合一下方法：

    Glide  
    .with( context )
    .load( eatFoodyImages[0] )
    .diskCacheStrategy( DiskCacheStrategy.NONE )
    .skipMemoryCache( true )
    .into( imageViewInternet );

**自定义磁盘缓存行为**

我们之前提到的，Glide有很多磁盘缓存的策略。在我们展示这些选项前，你可能意识到Glide的磁盘缓存是相当复杂的。例如，Picasso只缓存全尺寸图片。Glide，会缓存原始，全尺寸的图片和额外的小版本图片。例如，如果你请求一个1000x1000像素的图片，你的ImageView是500x500像素，Glide会保存两个版本的图片到缓存里。

现在，你应该明白.diskCacheStrategy()中枚举参数的意义了：

- DiskCacheStrategy.NONE 啥也不缓存

- DiskCacheStrategy.SOURCE 只缓存全尺寸图. 上面例子里的1000x1000像素的图片

- DiskCacheStrategy.RESULT 只缓存最终降低分辨后用到的图片

- DiskCacheStrategy.ALL 缓存所有类型的图片 (默认行为)

作为最后一个例子，如果你有一个图片你需要经常处理它，会生成各种不同的版本的图片，缓存它的原始的分辨率图片才有意义。这样，我们使用DiskCacheStrategy.SOURCE去告诉Glide只缓存原始版本：

    Glide  
    .with( context )
    .load( eatFoodyImages[2] )
    .diskCacheStrategy( DiskCacheStrategy.SOURCE )
    .into( imageViewFile );

##
###到了这里基本上上边这些知识已经满足于你的日常开发了，如果开发过程中实在解决不了可以点击下边这个链接，你想要的这里都有

