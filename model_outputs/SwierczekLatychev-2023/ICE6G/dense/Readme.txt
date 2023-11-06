
        1D Earth Model
        ==============

PREM: (Vp, Vs, Density) all major discontinuities are honored
96 km elastic LT
VM5a radial viscosity profile simplified (see below)
Radius [m]  Viscosity [Pa s]
3480000.0       3.16d21
5173800.9       3.16d21
5173800.9       1.58d21
5701000.0       1.58d21
5701000.0       0.5d21
6371000.0       0.5d21
where at R={ 5173.0 km, 5701.0 km} viscosity profile is discontinuous

        3D Earth Model
        ==============

Lithosphere

The elastic structure remains 1D, except the elastic LT is variable.
The average is ~ 96 km, but it may be +- a few km because of the mapping
between grids and introduction of plate boundaries (see next).
See file LAB.llz which gives the LAB depth (to the base of elastic LT)
as a surface elevation function (Lon, Lat, Depth). At each such Lat-Lon
we assign an "infinite viscosity" to all computational grid points above
"Depth". The original surface sampling is 1/2 degree on sphere. Note that
both poles are included as lines of constant values and there is an overlap
at Greenwich, i.e. along each latitude from +90 to -90, we begin at Lon=0
and end at Lon=360, then descend to the next latitude.

Plate boundaries

Lithosphere is "broken" along the plate boundaries. Their Lat-Lon surface
network coordinates are taken from the older version of P.Bird website
and resampled from ~100 km to ~5 km inter-point spacing
* the new version of the website  offers an ecripted data + tools to do so,
* but does not give simple Lat-Lon data points
See file PBnetM.dat, which begins like this:
           1
           1
       48695
   359.56209999999999       -54.851799999999997     
   359.62776615294752       -54.827587781885825     
   359.69278808554873       -54.802840944246327     
   359.75661585834524       -54.777116822322540     
   359.81873946295059       -54.750073617121728     
   359.87872012063718       -54.721495084572780     
   359.93622020473367       -54.691291641549043     
   359.99106427074008       -54.659505276721205     
   4.3898387310821255E-002  -54.626619982681689     
   9.5876229455225281E-002  -54.593302564544672     
  0.14807367984897304       -54.560123277068357     
  0.20167349448958777       -54.5277292949336
................

Ignore the first two lines. The third one gives the number of points (48695)
and then we list the points as Lon Lat pairs (Lon is first). The ranges are [0,360]
and [-90, +90], respectively.
Naturally, the data is groupped by "segments" and there is no apparent order,
so a fine sampling is essential not to miss a junction between them or to create
a toilet-paper style holes in the lithosphere.  A usual process
is to attach a tolerance sphere and ensure that the adjacent radii overlap when
mapping this onto a computational grid. We assume that the break is no wider than 72 km,
otherwise the width is proportional to the LAB depth (the radii of the tolerance spheres
would depend on the LAB model above, but no wider than 72 km, i.e. the tolerance radius
is limited to 72/2=36 km). Away from slabs, all LT breaks are vertical from the surface
to the LAB. 
*Near slabs, the breaks are following the upper slab surface, so they are
*titled and the original PB network may is adjusted. Let's leave this complication
* for now (i.e. no slabs and no adjustments for tilt and location)
* Major slabs are somehow captired by the LT and tomography in this setup
Within the plate boundaries, we assign a finite viscosity value of 0.17e21 Pa s,
which is ~ 1/3 of the upper mantle value (0.5e21 Pa s).

Viscosity

File stp_model_MH gives Log10(Nu_3D/Nu_1D) on 64 spherical surfaces dimensioned
361 x 721. The beginning of the file reads (hand inserted annotations after the "!")

           0           0           0           4        ! ignore this line
          64         361         721                    ! dimensions nR, nLat, nLon
   3529844.8275852134                                   ! model starts at this radius
   3579689.6551732332     
   3630000.0000001593     
   3680600.7067161961     
   3731678.4452284789     
   3782756.1837463002     
   3833833.9222643408     
   3884911.6607737052     
   3935989.3992920252     
   3987067.1378111225     
   4038144.8763197693     
   4089222.6148381047     
   4140300.3533601197     
   4191378.0918649184     
   4242455.8303846112     
   4293533.5689074276     
   4344611.3074277285     
   4395689.0459362986     
   4446766.7844472947     
   4497844.5229668254     
   4548922.2614788506     
   4599999.9999999795     
   4647816.7383413063     
   4695633.4766833223     
   4743450.2150231097     
   4791266.9533646740     
   4839083.6917068334     
   4886900.4300400838     
   4934717.1683821082     
   4982533.9067224814     
   5030350.6450644750     
   5078167.3834069902     
   5125984.1217193445     
   5173800.8600617489     
   5221617.5984023437     
   5269434.3367466619     
   5317251.0750837410     
   5365067.8134262906     
   5412884.5517608803     
   5460701.1908695772     
   5508518.0284431102     
   5553953.0267791180     
   5599999.9999999907     
   5666000.0000000447     
   5701000.0000000000     
   5735000.0000000000     
   5770999.9999979064     
   5820757.8000080064     
   5871700.0000000382     
   5922000.0000025043     
   5971000.0000004964     
   6021872.5868830848     
   6070243.2432555696     
   6118613.8996283030     
   6151000.0000000009     
   6171000.0000021253     
   6190999.9999730987     
   6210999.9999932265     
   6231000.0000279173     
   6250999.9999719644     
   6274999.9999725968     
   6298499.9999915687     
   6322000.0000318373     
   6346599.9999736398           ! topmost radius 6346.6 (24.4 km depth; MOHO in PREM)
   1.26497376                   ! Log10 data begins
   1.26497376    
   1.26497376    
   1.26497376    
   1.26497376    
   1.26497376    
   1.26497376    
   1.26497376    
   1.26497376    
   1.26497376    
   1.26497376    
   1.26497376    
   1.26497376    
   1.26497376    
   1.26497376    
   1.26497376    
   1.26497376    
   1.26497376    
   1.26497376    

...............

The choice of radial structure reflect the computational grid layers (radii are in meters!!)
The very first value 1.2649 ... is at R=3530 km , Lat=90, Lon=0, i.e. "north pole"
at this radius and tells us that the viscosity there is ~ 1.26 order of magnitude higher than background. All data is stretched into 1D column. The first 361 x 721 entries belong to
R=3530 km, etc. Each lateral slice has the same layout as the LAB model: from the NP to SP,
going from 0 to 360 along each latitude. Attaching Lat Lon Depth seems like a huge waste.

        Results
        =======
        
There are attached in two tarballs 1D.tar and 3D.tar for the 1D/3D models, resp.
THe loading is ICE-6G and we do the full cycle (three bathymetry iterations to determine
initial topography. Rotation is included.
Each tarball contains three sets of output files R_*, G_* and SL_*, (for radial displacement,
geoid change and sea level change, respectively) where *={01, 02, 25}.
The two-digit tag reflects the output time from 120 kybp to 250y inti the future,
but the selection is highly non-uniform. See file tt_25.dat for the actual mapping to the
time axis. The reason to include present +- 250 years at the end is to compute the present-day rates if needed. The full original output contains 267 files (time slices) saved on GL-512
from where we select 25 key frames and interpolate them onto GL-256 (coordinate file gl256 attached).


 
