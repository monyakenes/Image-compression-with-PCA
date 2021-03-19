# PCA
install.packages("jpeg")
library(jpeg)
sunflower <- readJPEG('sunflower.jpg')
ncol(sunflower)
## [1] 340
nrow(sunflower)
## [1] 403

r <- sunflower[,,1]
g <- sunflower[,,2]
b <- sunflower[,,3]

sunflower.r.pca <- prcomp(r, center = FALSE)
sunflower.g.pca <- prcomp(g, center = FALSE)
sunflower.b.pca <- prcomp(b, center = FALSE)

rgb.pca <- list(sunflower.r.pca, sunflower.g.pca, sunflower.b.pca)

str(sunflower.r.pca$rotation)
num = c(340)  

for (i in num) {                           
     pca.img <- sapply(rgb.pca, function(j) {
         compressed.img <- j$x[,11:100] %*% t(j$rotation[,11:100])
       }, simplify = 'array')
     writeJPEG(pca.img, paste('sunflower_PCA_',i,'_Princinpal.jpg', sep = ''))
   }
a <- summary(sunflower.r.pca)$importance
b <- summary(sunflower.g.pca)$importance
c <- summary(sunflower.b.pca)$importance
a[,1:8]
b[,1:8]
c[,1:8]
