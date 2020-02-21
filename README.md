
<!doctype html>

<html>
<head>
  <meta name="viewport" content="width=device-width, minimum-scale=1.0, initial-scale=1.0, user-scalable=yes">
  <meta name="theme-color" content="#4F7DC9">
  <meta charset="UTF-8">
  <title>ANDROID MVVM - part 1 UI</title>
  <link rel="stylesheet" href="//fonts.googleapis.com/css?family=Source+Code+Pro:400|Roboto:400,300,400italic,500,700|Roboto+Mono">
  <link rel="stylesheet" href="//fonts.googleapis.com/icon?family=Material+Icons">
  <link rel="stylesheet" href="https://storage.googleapis.com/codelab-elements/codelab-elements.css">
  <style>
    .success {
      color: #1e8e3e;
    }
    .error {
      color: red;
    }
  </style>
</head>
<body>
  <google-codelab-analytics gaid="UA-49880327-14"></google-codelab-analytics>
  <google-codelab codelab-gaid=""
                  id="building-a-view"
                  title="ANDROID MVVM - part 1 UI"
                  environment="web"
                  feedback-link="https://sagaj.io">
    
      <google-codelab-step label="Welcome" duration="1">
        <p>This is the first part of android MVVM(Model-View-ViewModel) implementation tutorial that will cover only UI implementation with no ViewModel or Model involved.</p>
<p>For complete detail about this tutorial, see the <a href="www.ubimemes.com" target="_blank"><em>MVVM tutorial</em></a></p>
<aside class="special"><p><strong>Note</strong>: This guidance is intended to help beginners to understand how android MVVM works and if you are higher level of that, you may want to skip this part and go to next tutorial.</p>
</aside>
<p><code>nano</code><a href="http://www.ubimemes.com" target="_blank">Ubimemes</a></p>
<p>If you run into any issues (code bugs, grammatical errors, unclear wording, etc.) as you work through this codelab, please report the issue via the ‘Report a mistake&#39; link in the lower left corner of the codelab.</p>
<h2 is-upgraded>Introduction</h2>
<p>안드로이드 View(UI)는 Activity와 Fragment로 구성됨. A Fragment is a self-contained component with its own user interface (UI) and lifecycle that can be reused in different parts of an app&#39;s UI. (A Fragment can also be used without a UI, in order to retain values across configuration changes, but this lesson does not cover that usage.)</p>
<p>A Fragment can be a static part of the UI of an Activity, which means that the Fragment remains on the screen during the entire lifecycle of the Activity. However, the UI of an Activity may be more effective if it adds or removes the Fragment dynamically while the Activity is running.</p>
<p>One example of a dynamic Fragment is the DatePicker object, which is an instance of DialogFragment, a subclass of Fragment. The date picker displays a dialog window floating on top of its Activity window when a user taps a button or an action occurs. The user can click OK or Cancel to close the Fragment.</p>
<p class="image-container"><img alt="Date Picker Fragment" src="img/b34e3ada556517c0.png"></p>
<p>building a view only - no data is attached at this step You&#39;ll learn about Navigation Component</p>
<h2 is-upgraded>What you should already know</h2>
<p>You should be able to:</p>
<ul>
<li>Create and run apps in Android Studio.</li>
<li>Use the layout editor to create a UI with a ConstraintLayout</li>
</ul>
<h2 class="checklist" is-upgraded>What you&#39;ll learn</h2>
<ul class="checklist">
<li>Add a Fragment to the layout of an Activity</li>
<li>Create a Navigation component</li>
</ul>
<h2 is-upgraded>What you&#39;ll do</h2>
<ul>
<li>Create Fragments to use as a UI element.</li>
<li>Add a RecyclerView to show word list</li>
<li>Add interactive elements to the Fragments that users can navigate among them</li>
</ul>


      </google-codelab-step>
    
      <google-codelab-step label="App overview" duration="1">
        <p>MVVM의 명확한 demonstration을 위해 일체의 데이터 연동 없이 UI(View)의 천이만 구현함 자동 생성되는 코드를 최대한 유용하여 Navigation Component를 이해하는 데 포커스 함</p>
<p class="image-container"><img alt="frag_main" src="img/92a45039d30bc9e0.jpg"><img alt="frag_dic_list" src="img/ebffeb5a5bc7cf4c.jpg"><img alt="frag_dic_detail" src="img/25bbed462cab4a7f.jpg"></p>
<h2 is-upgraded>View</h2>
<ol type="1">
<li>Create an Activity</li>
<li>Create Fragments</li>
</ol>
<h2 is-upgraded>Navigation</h2>
<ul>
<li>Automatic handling of fragment transactions</li>
<li>Android Studio tooling for visualizing and editing the navigation flow of an app</li>
</ul>
<p class="image-container"><img alt="navigation" src="img/2e3dff480efde8d5.png"></p>
<h2 is-upgraded>Create MainActivity</h2>
<pre><code>class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
    }
}
</code></pre>
<h2 is-upgraded>Edit XML layout (activity_main.xml)</h2>
<p>delete ‘Hello World&#39; TextView and add navigation framework</p>
<p>Your <code>activity_main.xml</code> file looks like below.</p>
<pre><code>&lt;?xml version=&#34;1.0&#34; encoding=&#34;utf-8&#34;?&gt;
&lt;androidx.constraintlayout.widget.ConstraintLayout 
    xmlns:android=&#34;http://schemas.android.com/apk/res/android&#34;
    xmlns:app=&#34;http://schemas.android.com/apk/res-auto&#34;
    xmlns:tools=&#34;http://schemas.android.com/tools&#34;
    android:layout_width=&#34;match_parent&#34;
    android:layout_height=&#34;match_parent&#34;
    tools:context=&#34;.MainActivity&#34;&gt;

    &lt;fragment
        android:id=&#34;@+id/nav_host_fragment&#34;
        android:name=&#34;androidx.navigation.fragment.NavHostFragment&#34;
        app:layout_constraintBottom_toBottomOf=&#34;parent&#34;
        app:defaultNavHost=&#34;true&#34;
        app:navGraph=&#34;@navigation/main&#34;
        android:layout_width=&#34;match_parent&#34;
        android:layout_height=&#34;match_parent&#34; /&gt;

&lt;/androidx.constraintlayout.widget.ConstraintLayout&gt;
</code></pre>
<p>Android Studio gives you an error for <code>NavHostFragment</code> since you didn&#39;t update gradle files for Android Navigation component yet. Later in this tutorial, you will update gradle files and the error will be gone.</p>
<h2 is-upgraded>Create WordListFragment</h2>
<h2 is-upgraded>Update gradle files</h2>
<p>This tutorial is experimented on version 2.3.0-alpha01 of navigation-fragment and if you use different version of it, the result may happen to be different.</p>
<pre><code>def nav_version = &#39;2.3.0-alpha01&#39;           // define the version of navigation-fragment

...

implementation &#34;androidx.navigation:navigation-fragment-ktx:$nav_version&#34;
...

</code></pre>
<h2 is-upgraded>Create Fragments</h2>
<p>You will create three Fragments as below.</p>
<ul>
<li>MainFragment</li>
<li>WordListFragment</li>
<li>WordDetailFragment</li>
</ul>
<h2 is-upgraded>Add a RecyclerView to a Fragment</h2>
<h2 is-upgraded>Create an Adapter for RecyclerView</h2>


      </google-codelab-step>
    
      <google-codelab-step label="Task 2. Navigations between Fragments" duration="10">
        <h2 is-upgraded>Create Navigation XML</h2>


      </google-codelab-step>
    
      <google-codelab-step label="Summary" duration="1">
        

      </google-codelab-step>
    
      <google-codelab-step label="Further explorations (or Learn more)" duration="5">
        

      </google-codelab-step>
    
  </google-codelab>

  <script src="https://storage.googleapis.com/codelab-elements/native-shim.js"></script>
  <script src="https://storage.googleapis.com/codelab-elements/custom-elements.min.js"></script>
  <script src="https://storage.googleapis.com/codelab-elements/prettify.js"></script>
  <script src="https://storage.googleapis.com/codelab-elements/codelab-elements.js"></script>

</body>
</html>
