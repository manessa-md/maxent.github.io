```
#Step 1 BIO-ORAcle dataset
#biophysic parameter
# exploring the marine datasets 
datasets <- list_datasets(terrestrial = FALSE, marine = TRUE)

layers <- list_layers(datasets)

# download pH and Salinity to the temporary directory
load_layers(layers[layers$name %in% c("Bathymetry (mean)", "Chlorophyll A (range)") & 
                     layers$dataset_code == "Bio-ORACLE",], datadir = tempdir())

# set a default datadir, preferably something different from tempdir()
options(sdmpredictors_datadir= tempdir())

# (down)load specific layers 
biom <- load_layers(c("BO_chlorange", "BO_bathymean"))


#Step 1 data
"Rhincodon typus"
sp = gbif("Rhincodon", "typus", download = T, geo=T,sp=F)

w = which(is.na(sp$lon))
sp = sp[-w,]
sp$species = 1
sp = sp[,c('lon','lat','species')]
head(sp)
coordinates(sp) = ~lon + lat


#plot data
plot(biom[[1]])
points(sp, cex=0.5, pch=16)

#model
d = sdmData(species~., sp, predictors = biom, bg = list(n=100, method='eRandom'))
d

m = sdm(species~., d, methods=c('glm', 'svm','rf'), 
        replication = c('boot'), n=2)
m

gui(m)

m = sdm(species~., d, methods=c('rf'),  replication = c('boot'), n=2)
m

p             <- predict(m, biom)
extent(p)     <- extent(biom)
projection(p) <- projection(biom)
plot(p$id_1.sp_1.m_rf.re_boot)

writeRaster(p, filename="pr.tif", format="GTiff", overwrite=TRUE) 


```
