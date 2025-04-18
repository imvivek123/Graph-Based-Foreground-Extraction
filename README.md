<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Graph-Based Foreground Extraction</title>
</head>
<body>

  <h1>🖼️ Graph-Based Foreground Extraction</h1>

  <h2>Graph-Based Image Segmentation using Max-Flow/Min-Cut</h2>

  <p>This project implements <strong>interactive image segmentation</strong> using the <strong>Graph Cut</strong> method. The user provides an input image and a seed image where foreground (object) and background regions are manually marked. The program constructs a graph where each pixel is a node, applies a max-flow algorithm (Ford-Fulkerson), and segments the image into foreground and background using min-cut.</p>

  <h4>🎨 Seed colors:</h4>
  <ul>
    <li><strong>Red</strong> pixels represent foreground seeds.</li>
    <li><strong>Green</strong> pixels represent background seeds.</li>
  </ul>

  <h3>📌 Introduction</h3>

  <p>Image segmentation is a fundamental task in computer vision where the goal is to partition an image into meaningful regions. This project uses a graph-based approach where:</p>
  <ul>
    <li>Each pixel is a node.</li>
    <li>Edges (with weights based on color similarity and user input) are drawn between neighboring pixels and between each pixel and two special nodes: <strong>Source</strong> (foreground) and <strong>Sink</strong> (background).</li>
    <li>A <strong>max-flow/min-cut algorithm</strong> is applied to segment the image based on the minimum energy cost.</li>
  </ul>

  <h4>Key components:</h4>
  <ul>
    <li>Grayscale image conversion</li>
    <li>Graph construction with T-links and N-links</li>
    <li>Seed-based probabilistic modeling (Gaussian estimation)</li>
    <li>Ford-Fulkerson or other max-flow algorithm variants for segmentation</li>
    <li>Timing analysis of major steps</li>
  </ul>

  <h3>⚙️ How to Run This Project</h3>

  <h4>1. Install Dependencies</h4>
  <p>You must have <strong>OpenCV</strong> installed on your system. It is used for image input/output, color space conversion, and drawing.</p>

  <p>Install OpenCV using:</p>
  <ul>
    <li><a href="https://docs.opencv.org/master/d7/d9f/tutorial_linux_install.html">OpenCV installation guide for Linux</a></li>
    <li><a href="https://docs.opencv.org/master/d3/d52/tutorial_windows_install.html">OpenCV installation guide for Windows</a></li>
  </ul>

  <h4>2. Clone the Repository</h4>
  <pre><code>
git clone https://github.com/tashir0605/Graph-Based-Foreground-Extraction
cd Graph_Based_Image_Segmentation
  </code></pre>

  <h4>3. Build the Project</h4>
  <pre><code>
mkdir build && cd build
cmake ..
make -j8
make install
  </code></pre>

  <h5>🛠️ Troubleshooting</h5>
  <ul>
    <li>If you get dependency errors during configuration, create a <code>3rdparty/lib</code> folder and place the required <code>.lib</code> or <code>.so</code> files there.</li>
    <li>If configuration or compilation fails, try upgrading CMake or your compiler.</li>
    <li>To change the default installation path, use:
      <pre><code>cmake .. -DCMAKE_INSTALL_PREFIX=/your/custom/path</code></pre>
    </li>
  </ul>

  <h3>🚀 Usage</h3>
  <p>After building, you can run the segmentation program from the terminal:</p>
  <pre><code>
./GraphCutter input.jpg seed.jpg output.jpg mask.jpg
  </code></pre>

  <h4>Where:</h4>
  <ul>
    <li><code>input.jpg</code> is the original image.</li>
    <li><code>seed.jpg</code> is the image with red and green seed labels.</li>
    <li><code>output.jpg</code> will contain the segmented foreground object.</li>
    <li><code>mask.jpg</code> will contain the binary segmentation mask.</li>
  </ul>

  <h4>Example Output (Terminal View):</h4>
  <pre><code>
tashir@vict:~/Graph Based Image Segmentation/Input seed$ ../build/GraphCutter input.jpg seed.jpg output.jpg mask.jpg
Create N-Links: 0.164004s
Create T-Links: 0.135021s
Max Flow: 129.082s
  </code></pre>

  <h3>🧠 API and Library Usage</h3>

  <p>If you want to integrate this into your own C++ project, you can use the exposed API:</p>

  <pre><code>
static void cutImage(cv::InputArray image, cv::OutputArray result, cv::OutputArray mask,
    const std::vector<cv::Point>& foreSeeds, const std::vector<cv::Point>& backSeeds,
    float lambda = 0.01f, float sigma = -1.0, PerfMetric* perfMetric = nullptr);
  </code></pre>

  <h4>Parameters:</h4>
  <ul>
    <li><code>image</code>: Input image (color or grayscale)</li>
    <li><code>result</code>: Output segmented image (foreground only)</li>
    <li><code>mask</code>: Binary mask of the segmentation result</li>
    <li><code>foreSeeds</code>: Vector of foreground seed pixel coordinates</li>
    <li><code>backSeeds</code>: Vector of background seed pixel coordinates</li>
    <li><code>lambda</code>: Balances the region and boundary terms</li>
    <li><code>sigma</code>: Controls smoothness (set to -1 to auto-compute)</li>
    <li><code>perfMetric</code>: Optional pointer to performance logger</li>
  </ul>

</body>
</html>

