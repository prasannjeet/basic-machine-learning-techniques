Exercise 1 k-NN Classification
==============================

Created By: **Prasannjeet Singh**

This file contains solution 1 through 6 of the first exercise of
Assignment - 1.

**Notes**

<div>

-   All the function implementations are done in external files, which
    are all included within this folder. More details about each
    implemented function can be found in their respective .m files.
-   Console outputs are shown in black background and white text.

</div>

Contents
--------

<div>

-   [**Q1 Plotting the training data in a scatter-plot.**](#1)
-   [**Q2 Implementing kNNclassify algorithm**](#2)
-   [**Q3 Classifying (-17, 14) for k=1,3 and 5.**](#3)
-   [**Q4 kNNdrawBoundary Implementation and Plotting**](#4)
-   [**Q5 The Training Error**](#5)
-   [**Q6 kNNclassify\_taxi Implementation, Classification and Boundary
    with different values of k \[1, 3, 5\]**](#8)

</div>

**Q1 Plotting the training data in a scatter-plot.** {#1}
----------------------------------------------------

Plotting uses the function **plotTrainingData()** which is defined in
this folder. More about the function can be read in it\'s function
definition.

``` {.codeinput}
load Data/data1.mat;
plotTrainingData(X, y, 65);
snapnow;
close;
```

![](Exercise1_01.png)

**Q2 Implementing kNNclassify algorithm** {#2}
-----------------------------------------

The function **kNNclassify()** has been implemented in this folder. More
about the function can be read in it\'s function definition.

**Q3 Classifying (-17, 14) for k=1,3 and 5.** {#3}
---------------------------------------------

Classifying the points uses **kNNclassify()** function. More about it
can be read in it\'s function definition.

``` {.codeinput}
load Data/data1.mat;
hFig = figure(3);
set(hFig, 'Position', [0 0 1500 500]);
for i = 1:3
    subplot(1,3,i);
    [~,~,OutputMessage] = kNNclassify (i*2-1, X, y, [-17, 14])
end
snapnow
close(hFig);
```

``` {.codeoutput}
OutputMessage =

    'For k =1, and point = (-17,14)
     New Point Belongs to Group [1] (or RED) Category
     The point has been marked in pink
     The boundary has also been marked with the color red'


OutputMessage =

    'For k =3, and point = (-17,14)
     New Point Belongs to Group [1] (or RED) Category
     The point has been marked in pink
     The boundary has also been marked with the color red'


OutputMessage =

    'For k =5, and point = (-17,14)
     New Point Belongs to Group [0] (or BLUE) Category
     The point has been marked in light blue
     The boundary has also been marked with the color blue'
```

![](Exercise1_02.png)

**Q4 kNNdrawBoundary Implementation and Plotting** {#4}
--------------------------------------------------

The boundary is drawin using the function **kNNdrawBoundary()** which
has been implmented in this folder. It uses the contour() function to
draw the boundary. More about it can be read in the function definition
which is in this folder.

``` {.codeinput}
load Data/data1.mat;
hFig = figure(1);
set(hFig, 'Position', [0 0 1500 500]);
for i = 1:3
    subplot(1,3,i);
    kNNdrawBoundary(i*2-1, X, y);
end
snapnow;
close(hFig);
```

![](Exercise1_03.png)

**Q5 The Training Error** {#5}
-------------------------

To calculate the training error, I check whether a particular value of k
can accurately classify an already existing point in the graph. I did
this by using the method **trainingError()** which is implemented and
defined in this folder. Moreover, I have also plotted a graph which maps
the training error for each value of \'k\'. This was done by the
function **trainingErrorMatrix()** which is also implemented and defined
in this folder.

*Let us see this graph for a broad understanding:*

``` {.codeinput}
load Data/data1.mat;
[~,trainingErrorGraph] = trainingErrorMatrix(X,y);
snapnow;
close;
```

![](Exercise1_04.png)

Just by looking at the image above, we can say that in most of the cases
the training error increases as we increase the value of k. Note that
the k value is always odd in the above graph. Let us also make a table
with precise values of training error for a few values of k:

  k    Training Error
  ---- ----------------
  1    0.000
  3    8.333
  5    11.667
  7    15.000
  9    15.000
  11   16.667

From the table above, it can be noticed that there is absolutely no
training error when the value of k is 1, however, k=1 is **not** the
best choice for generalization of the model to unseen points, because no
matter what manner the points are scattered in the graph, the training
error for k=1 will always be zero, because for any particular point,
that point itself will always be the nearest (with distance = 0). This
observation tells us that k=1 is a clear case of **overfitting**, and
while training results might be the best in overfitting, test-results
aren\'t. Moreover, any **outlier** values have a high chance of always
being wrongly classified.

Therefore a relatively larger value of k has a high probability of
classifying test data better than k=1. However, we cannot also have a
very high value of k, as the training error peaks as we keep increasing
the value of k. Therefore, a value between 3 to 7 should be optimal in
the above scenario.

**Q6 kNNclassify\_taxi Implementation, Classification and Boundary with different values of k \[1, 3, 5\]** {#8}
-----------------------------------------------------------------------------------------------------------

Drawing boundary for Taxi-Cab algorithm uses the same function as
drawing boundary for Euclidean algorithm **kNNdrawBoundary()**. Using
the optional fourth argument, we can draw the Taxi-Cab boundary. More
details about the optional argument, etc. can be read in the function
definition which is present in this same folder.

**Classification of the point (-17, 14) for various values of k**

``` {.codeinput}
load Data/data1.mat;
hFig = figure(6);
set(hFig, 'Position', [0 0 1500 500]);
for i = 1:3
    subplot(1,3,i);
    [~,~,OutputMessage] = kNNclassify_taxi (i*2-1, X, y, [-17, 14])
end
snapnow
close(hFig);
```

``` {.codeoutput}
OutputMessage =

    'For k =1, and point = (-17,14)
     New Point Belongs to Group [1] (or RED) Category
     The point has been marked in pink
     The boundary has also been marked with the color red'


OutputMessage =

    'For k =3, and point = (-17,14)
     New Point Belongs to Group [0] (or BLUE) Category
     The point has been marked in light blue
     The boundary has also been marked with the color blue'


OutputMessage =

    'For k =5, and point = (-17,14)
     New Point Belongs to Group [1] (or RED) Category
     The point has been marked in pink
     The boundary has also been marked with the color red'
```

![](Exercise1_05.png)

**Let us now compare the classifications done by Taxi-Cab algorithm and
Euclidean algorithm:**

  k   Euclidean Algorithm   Taxi-Cab Algorithm
  --- --------------------- --------------------
  1   1                     1
  3   1                     0
  4   0                     1

As we can see, except at k=1, both the algorithms produce different
results.

**Drawing The Boundary for This Algorithm in Comparision with Euclidean
Algorithm**

*Note that the small dots scattered in the graph are the original
points* *from the data1.m file. These are plotted along with the
boundary for* *reference.*

``` {.codeinput}
load Data/data1.mat;
for i = 1:3
    kNNdrawBoundary(i*2-1, X, y, 1);
    snapnow;
    hold off;
    close;
end
```

![](Exercise1_06.png) ![](Exercise1_07.png) ![](Exercise1_08.png)

Exercise 2 - Multi Class k-NN
=============================

Submitted by **Prasannjeet Singh**

This file contains solution 1 to 3 of Exercise-2 of Assignment 1.

**Notes**

<div>

-   All the function implementations are done in external files, which
    are all included within this folder. More details about each
    implemented function can be found in their respective .m files.
-   Console outputs are shown in black background and white text.

</div>

Contents
--------

<div>

-   [Q1 Plotting the training data in a ScatterPlot](#1)
-   [Q2 Drawing the Decision Boundary](#2)
-   [Q3 Finding the Error Rate from Test Data](#3)

</div>

Q1 Plotting the training data in a ScatterPlot {#1}
----------------------------------------------

This can simply be done by using the inbuilt **gscatter()** function:

``` {.codeinput}
clear all;
load Data/data2.mat;
thisFig = figure(1);
gscatter(train_X(:,1),train_X(:,2), train_y, 'brgk', 'phd*');
snapnow;
close(thisFig);
```

![](Exercise2_01.png)

Q2 Drawing the Decision Boundary {#2}
--------------------------------

This uses the function **kNNdrawBoundary\_multiclass()** which is
defined in this folder. More details about the function can be read in
it\'s file.

``` {.codeinput}
load Data/data2.mat;
thisFig = figure(2);
set(thisFig, 'Position', [0 0 2000 500]);
for i = 1:4
    subplot(1,4,i);
    kNNdrawBoundary_multiclass (i*2-1, train_X, train_y);
end
snapnow;
close(thisFig);
```

![](Exercise2_02.png)

Q3 Finding the Error Rate from Test Data {#3}
----------------------------------------

This uses the **errorRateFinder()** function, which is defined in this
folder. More details about the function can be read in it\'s file.

**Plotting Error Rate vs *k* for the given test data**

``` {.codeinput}
% Initialization
load Data/data2.mat;
[rows, ~] = size(train_X);

% Running loop to find accuracy and error rates for each k
clearvars theMatrix;
theMatrix = ones(rows,2);
for i = 1:rows
    [~,er] = errorRateFinder(i,train_X,train_y,test_X,test_y);
    theMatrix(i,:) = [i, er];
end

% Now plotting the above generated matrix
hFig = figure(3);
set(hFig, 'Position', [0 0 1000 500]);
subplot('position',[0.05 0.1 0.95 0.85]);
graph = bar(theMatrix(:,1), theMatrix(:,2),'FaceColor',[0 .5 .5]);
title('Error Plotted Against k');
xlabel(strcat('k-Values ranging from',32,int2str(1),' to',32,int2str(rows)));
ylabel('The Training Errors');
snapnow;
close(hFig);
```

![](Exercise2_03.png)

As can be observed clearly, error increases gradually as we incease the
value of k. Moreover, after a certain value of k, the error peaks up and
then stays constant. Let us now find the value of k for which the error
was the least and also the error percentage for that k.

``` {.codeinput}
leastError = sortrows(theMatrix, 2);
kValue = leastError(1,1)
ErrorValue = leastError(1,2)
```

``` {.codeoutput}
kValue =

    29


ErrorValue =

    7.7922
```

**Therefore, the value of k with the smallest error (7.8%) is 29.**

Exercise 3: k-NN Regression
===========================

This document contains solutions for question 1 to 3 of Exercise-3.

Contents
--------

<div>

-   [Q1 Implementing k-NN Regression](#1)
-   [Q2 Testing the Regression Model](#2)
-   [Q3 Mean Squared Error](#4)

</div>

Q1 Implementing k-NN Regression {#1}
-------------------------------

The function **kNNregression()** has been implemented and is available
in this folder.

Q2 Testing the Regression Model {#2}
-------------------------------

Using the given sample data **z** Using the value of k as **12**

``` {.codeinput}
load Data/data3.mat;
kNNregression(12, train_X, train_y, z)
```

``` {.codeoutput}
ans =

   1.6156e+04
```

As can be observed, the answer matches with the one provided in the
assignment.

Q3 Mean Squared Error {#4}
---------------------

As Mean Squared Error is not explicitly defined in the question, it is
assumed to be the following:

![](https://wikimedia.org/api/rest_v1/media/math/render/svg/e258221518869aa1c6561bb75b99476c4734108e)

Taken from [This Wikipedia
Article.](https://en.wikipedia.org/wiki/Mean_squared_error)

``` {.codeinput}
load Data/data3.mat;
[rows, columns] = size(test_X);
for k = 1:10
    for i = 1:rows
        testResult(i,k) = kNNregression(k, train_X, train_y, test_X(i,:));
    end
end
testResult = ((sum((testResult-(repmat(test_y, [1,10]))) .^ 2))/rows)';
testResult(:,2) = 1:10;
thisFig = figure(3);
graph = bar(testResult(:,2), testResult(:,1),'FaceColor',[0 .5 .5],'EdgeColor',[0 .9 .9],'LineWidth',1.5);
title('Mean Squared Error for Different Values of k');
xlabel('k Values');
ylabel('Mean Squared Error');
snapnow;
close(thisFig);
```

![](Exercise3_01.png)

Now let us find the value of k that minimizes the test error

``` {.codeinput}
testResult = sortrows(testResult, 1);
kValue = testResult(1,2)
errorValue = testResult(1,1)
```

``` {.codeoutput}
kValue =

     4


errorValue =

   1.2405e+06
```

Therefore, as calculated, the least test error is observed with k = 4.

Exercise 4: Assignment 1
========================

This document contains the solution to VG exercise of the assignment 1.

Contents
--------

<div>

-   [Generating the Heat Map](#1)
-   [The Gradient Value and K](#2)
-   [Generating Heat-Map](#3)
-   [Plotting the Heat-Map in a 2-D graph](#4)
-   [Generating 3-D surface heat map](#6)

</div>

Generating the Heat Map {#1}
-----------------------

Note that I have used two features from the sample data provided to us
(data3.mat) to generate the heat map, as it might be insightful to
observe the heat-map of real data, rather than looking at the heatmap of
a randomly generated data.

The features used for generating heat-map are:

<div>

1.  Wheel-Base (Column *1* in data3.mat), and
2.  Engine-Size (Column *6* in data3.mat).

</div>

Both the data mentioned above are normalized in the function
implementation.

``` {.codeinput}
% Clearing the workspace, loading the data, then selecting the data-sets
% as described above.
clear all;
load Data/data3.mat
heatX = train_X(:,[1,6]);
```

The Gradient Value and K {#2}
------------------------

Gradient value can be specified below. The returned matrix will be a two
dimensional square matrix with dimensions G\*G. Thus, a total of G\*G
test sets are generated on which k-NN regression is applied and the
results are returned in a square matrix. **A higher value of G will
result in less-pixelated heat map, however, it will take longer to
execute.** No loops are used. The data sets will always be normalized in
the range of 0-G, as G will be the length and height of the graph. K was
randomly chosen to be 12. Both the values can be changed to see varied
results.

``` {.codeinput}
G = 500;
k = 12;
```

Generating Heat-Map {#3}
-------------------

Note that below function will accept any two features (from any data
source) to create a heat matrix, as long as there are only two features
and are distributed in two columns, and the second parameter contains
the training data solution.

``` {.codeinput}
[heatMatrix] = heatMapGenerator(k, heatX, train_y, G);
```

Plotting the Heat-Map in a 2-D graph {#4}
------------------------------------

Following is the generated graph:

``` {.codeinput}
hFig1 = figure(4);
h1 = axes;
imagesc(heatMatrix), colorbar, colormap(flipud(hot));
set(h1, 'XAxisLocation', 'Top');
title('Heat Map for Car Prices');
xlabel('Wheel-Base');
ylabel('Engine-Size');
snapnow;
close(hFig1);
```

![](Exercise4_01.png)

The heatmap generated above is exactly as we expected it to be. As can
be observed in the sample data, cost of the vehicle increase when
wheel-base or engine size is increased, we can observe the same trend in
the image above. Note that the range of X and Y axis are normalized
according to the value of G chosen by us.

**Additionally**, since I chose the value of G as 500, a lower value of
G would have created a pixelated graph as below. However, the trends
would not change.

``` {.codeinput}
heatMatrix2 = heatMatrix([1:ceil(G/100):G], [1:ceil(G/100):G]);
hFig2 = figure(5);
h1 = axes;
imagesc(heatMatrix2), colorbar, colormap(flipud(hot));
set(h1, 'XAxisLocation', 'Top');
title('Heat Map for Car Prices');
xlabel('Wheel-Base');
ylabel('Engine-Size');
snapnow;
close(hFig2);
```

![](Exercise4_02.png)

Generating 3-D surface heat map {#6}
-------------------------------

Note that to generate a surface plot, the size of the matrix had to be
proportionally minimized to reduce the enumber of edges (the black lines
in the graph that show the depth), which made the graph
un-interpretable. However, the trends shown will be exactly the same.

``` {.codeinput}
heatMatrix3 = heatMatrix([1:ceil(G/10):G], [1:ceil(G/10):G]);
hFig3 = figure(6);
h1 = axes;
surf(heatMatrix3), colorbar, colormap(flipud(hot));
set(h1, 'XAxisLocation', 'Top');
title('3-D Heat Map for Car Prices');
xlabel('Wheel-Base');
ylabel('Engine-Size');
snapnow;
close(hFig3);

% Rotated Graph

hFig4 = figure(7);
h1 = axes;
theGraph = surf(heatMatrix3); colorbar, colormap(flipud(hot));
set(h1, 'XAxisLocation', 'Top');
title('3-D Heat Map for Car Prices (Rotated)');
xlabel('Wheel-Base');
ylabel('Engine-Size');
direction = [0 0 1];
rotate(theGraph,direction,-75)
snapnow;
close(hFig4);
```

![](Exercise4_03.png) ![](Exercise4_04.png)

Function used to create the heat-map was **imagesc()**, and

The function used to create the 3d heat map was **surf()**.

I chose these functions as they don\'t require any new library
inclusions and moreover, they are easy to use. **surf()** can also be
easily rotated and snapped for different representations. Moreover, I
changed the colormap to **red** to signify that a *heatmap* is drawn.
However, I prefer the idea of representing the heatmap in two dimensions
as we already have color labels which makes us understand which area of
the graph has a higher price. Furthermore, using less data-sets to plot
the the heatmap, in a way, gave me an idea of how screen resolutions
(eg. in mobile-phones) work, where less dots per inches (dpi) phones
creates images with lesser quality as compared to phones with high dpi.

[Published originally with MATLAB R2018b](https://www.mathworks.com/products/matlab/)
