# Graph-Based-Foreground-Extraction
## Graph-Based Image Segmentation using Max-Flow/Min-Cut

This project implements **interactive image segmentation** using the **Graph Cut** method. The user provides an input image and a seed image where foreground (object) and background regions are manually marked. The program constructs a graph where each pixel is a node, applies a max-flow algorithm (such as Ford-Fulkerson), and segments the image into foreground and background using min-cut.

> Seed colors:
> - **Red** pixels represent foreground seeds.
> - **Green** pixels represent background seeds.

## 📌 Introduction

Image segmentation is a fundamental task in computer vision where the goal is to partition an image into meaningful regions. This project uses a graph-based approach where:
- Each pixel is a node.
- Edges (with weights based on color similarity and user input) are drawn between neighboring pixels and between each pixel and two special nodes: **Source** (foreground) and **Sink** (background).
- A **max-flow/min-cut algorithm** is applied to segment the image based on the minimum energy cost.

Key components:
- Grayscale image conversion
- Graph construction with T-links and N-links
- Seed-based probabilistic modeling (Gaussian estimation)
- Ford-Fulkerson or other max-flow algorithm variants for segmentation
- Timing analysis of major steps

## ⚙️ How to Run This Project

### 1. Install Dependencies

You must have **OpenCV** installed on your system. It is used for image input/output, color space conversion, and drawing.

Install OpenCV using:
- [OpenCV installation guide for Linux](https://docs.opencv.org/master/d7/d9f/tutorial_linux_install.html)
- [OpenCV installation guide for Windows](https://docs.opencv.org/master/d3/d52/tutorial_windows_install.html)

### 2. Clone the Repository

```bash
git clone https://github.com/peihaowang/InteractiveGraphCut.git
cd InteractiveGraphCut

3. Build the Project with CMake

mkdir build && cd build
cmake ..
make -j8
make install

🛠️ Troubleshooting

If you get dependency errors during configuration, create a 3rdparty/lib folder and place the required .lib or .so files there.
If configuration or compilation fails, try upgrading CMake or your compiler.
To change the default installation path, use:

cmake .. -DCMAKE_INSTALL_PREFIX=/your/custom/path

🚀 Usage
After building, you can run the segmentation program from the terminal:
./GraphCutter input.jpg seed.jpg output.jpg mask.jpg

Where:

input.jpg is the original image.
seed.jpg is the image with red and green seed labels.
output.jpg will contain the segmented foreground object.
mask.jpg will contain the binary segmentation mask.
Example Output (Terminal View):

tashir@vict:~/Graph Based Image Segmentation/Input seed$ ../build/GraphCutter input.jpg seed.jpg output.jpg mask.jpg
Create N-Links: 0.164004s
Create T-Links: 0.135021s
Max Flow: 129.082s

🧠 API and Library Usage
If you want to integrate this into your own C++ project, you can use the exposed API:

static void cutImage(cv::InputArray image, cv::OutputArray result, cv::OutputArray mask,
    const std::vector<cv::Point>& foreSeeds, const std::vector<cv::Point>& backSeeds,
    float lambda = 0.01f, float sigma = -1.0, PerfMetric* perfMetric = nullptr);

Parameters:

image: Input image (color or grayscale).
result: Output segmented image (foreground only).
mask: Binary mask of the segmentation result.
foreSeeds: Vector of foreground seed pixel coordinates.
backSeeds: Vector of background seed pixel coordinates.
lambda: Balances the region and boundary terms.
sigma: Controls smoothness (set to -1 to auto-compute).
perfMetric: Optional pointer to performance logger.

🧾 References

Boykov, Y., & Jolly, M. P. (2001). Interactive graph cuts for optimal boundary & region segmentation of objects in N-D images. ICCV.
Kolmogorov, V., & Zabih, R. (2004). What energy functions can be minimized via graph cuts? IEEE Transactions on Pattern Analysis and Machine Intelligence.

