
HOW TO RUN THE IMAGE PROCESSING BENCHMARK PROGRAMS


This project contains THREE ways to run the image processing benchmarks:

1. main.py              - Runs BOTH multiprocessing and concurrent.futures together
2. run_multiprocessing.py    - Runs ONLY multiprocessing benchmarks
3. run_concurrent_futures.py - Runs ONLY concurrent.futures benchmarks

================================================================================
PREREQUISITES
================================================================================

1. Ensure you have Python 3.7+ installed
2. Install required packages:
   
   pip install numpy pillow matplotlib

3. Place your input images (JPG format) in the ./input_images/ folder

================================================================================
OPTION 1: RUN BOTH PARADIGMS TOGETHER (Original)
================================================================================

Command:
    python main.py

Description:
    - Runs sequential baseline first
    - Tests BOTH multiprocessing AND concurrent.futures
    - Tests all three strategies (Pixel-Level, Image-Level, Task-Level)
    - Generates comparison charts and analysis
    
Output Files (in ./output_images/):
    - benchmark_output.txt      : Full log with analysis
    - benchmark_results.csv     : Tabular results for both paradigms
    - benchmark_results.json    : Structured data
    - performance.png           : Comparison charts

================================================================================
OPTION 2: RUN MULTIPROCESSING ONLY
================================================================================

Command:
    python run_multiprocessing.py

Description:
    - Runs sequential baseline first
    - Tests ONLY multiprocessing module
    - Uses: multiprocessing.Pool, pool.starmap, pool.apply_async
    - Tests all three strategies (Pixel-Level, Image-Level, Task-Level)
    
Output Files (in ./output_images/):
    - benchmark_multiprocessing.txt   : Log file
    - benchmark_multiprocessing.csv   : Results table
    - benchmark_multiprocessing.json  : Structured data
    - performance_multiprocessing.png : Charts

Key Features of Multiprocessing:
    - Lower-level control over process pools
    - pool.map() for simple parallel mapping
    - pool.starmap() for multiple arguments
    - pool.apply_async() with callbacks for pipelines

================================================================================
OPTION 3: RUN CONCURRENT.FUTURES ONLY
================================================================================

Command:
    python run_concurrent_futures.py

Description:
    - Runs sequential baseline first
    - Tests ONLY concurrent.futures module
    - Uses: ProcessPoolExecutor, executor.map, executor.submit
    - Tests all three strategies (Pixel-Level, Image-Level, Task-Level)
    
Output Files (in ./output_images/):
    - benchmark_concurrent_futures.txt   : Log file
    - benchmark_concurrent_futures.csv   : Results table
    - benchmark_concurrent_futures.json  : Structured data
    - performance_concurrent_futures.png : Charts

Key Features of Concurrent.Futures:
    - Higher-level, more Pythonic API
    - ProcessPoolExecutor for process-based parallelism
    - executor.submit() returns Future objects
    - as_completed() for handling results as they finish
    - Context manager support (with statement)

================================================================================
QUICK START EXAMPLES
================================================================================

# Run multiprocessing only:
cd C:\Users\msuha\OneDrive\Desktop\CST435-Assignment-2-Editted
python run_multiprocessing.py

# Run concurrent.futures only:
cd C:\Users\msuha\OneDrive\Desktop\CST435-Assignment-2-Editted
python run_concurrent_futures.py

# Run both together (original):
cd C:\Users\msuha\OneDrive\Desktop\CST435-Assignment-2-Editted
python main.py

================================================================================
COMPARISON: MULTIPROCESSING vs CONCURRENT.FUTURES
================================================================================

Feature                  | multiprocessing        | concurrent.futures
-------------------------|------------------------|-------------------------
API Level                | Lower-level            | Higher-level (Pythonic)
Pool Creation            | Pool(processes=n)      | ProcessPoolExecutor(n)
Simple Mapping           | pool.map()             | executor.map()
Multiple Args            | pool.starmap()         | (use submit + loop)
Async with Callback      | pool.apply_async()     | executor.submit()
Result Handling          | Callback functions     | Future objects
Completion Order         | Callbacks fire on done | as_completed() iterator
Context Manager          | Supported              | Supported (recommended)
Performance              | ~Same (both use pools) | ~Same (both use pools)

================================================================================
PARALLELIZATION STRATEGIES TESTED
================================================================================

1. PIXEL-LEVEL:
   - Divides each image into horizontal chunks (rows)
   - Each worker processes a portion of pixels
   - Good for: Very large images, fine-grained parallelism
   
2. IMAGE-LEVEL:
   - Each worker processes a complete image independently
   - Simple coarse-grained parallelism
   - Good for: Many small images
   
3. TASK-LEVEL (Pipeline):
   - Processing stages execute asynchronously
   - Multiple images can be in different pipeline stages
   - Good for: Maximizing throughput, overlapping computation

================================================================================
EXPECTED OUTPUT STRUCTURE
================================================================================

After running, your output_images/ folder will contain:

./output_images/
├── output.jpg                          (processed image)
├── benchmark_output.txt                (main.py log)
├── benchmark_results.csv               (main.py results)
├── benchmark_results.json              (main.py data)
├── performance.png                     (main.py charts)
├── benchmark_multiprocessing.txt       (multiprocessing log)
├── benchmark_multiprocessing.csv       (multiprocessing results)
├── benchmark_multiprocessing.json      (multiprocessing data)
├── performance_multiprocessing.png     (multiprocessing charts)
├── benchmark_concurrent_futures.txt    (futures log)
├── benchmark_concurrent_futures.csv    (futures results)
├── benchmark_concurrent_futures.json   (futures data)
└── performance_concurrent_futures.png  (futures charts)

================================================================================
TROUBLESHOOTING
================================================================================

1. "No images found" error:
   - Ensure JPG images exist in ./input_images/ folder
   
2. Import errors:
   - Run: pip install numpy pillow matplotlib
   
3. Permission errors on Windows:
   - Run command prompt as Administrator
   
4. Slow performance:
   - Reduce number of images for testing
   - Check that images are reasonable size (not extremely large)

================================================================================
