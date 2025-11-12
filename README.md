
# Caracterización molecular y filogenética de poblacional de la familia *Psychotria* (*Rubiaceae*)

El presente proyecto tuvo como objetivo realizar una caracterización filogenética y poblacional del género *Psychotria* (Familia *Rubiaceae*), mediante el análisis de secuencias del gen cloroplástico rbcL obtenidas de la base de datos GenBank. Se recopilaron más de 20 accesiones representativas de distintas especies del género, priorizando aquellas de distribución tropical. Las secuencias fueron sometidas a control de calidad para eliminar duplicados, secuencias incompletas y regiones ambiguas. Posteriormente, se realizó un alineamiento múltiple utilizando el programa MAFFT, seguido de la estimación de distancias genéticas y la construcción de árboles filogenéticos bajo el método de Máxima Verosimilitud con soporte bootstrap. Adicionalmente, se aplicaron análisis poblacionales básicos y multivariados (PCA y AMOVA) para evaluar la estructura genética entre especies y regiones geográficas. Los resultados evidencian una clara diferenciación entre clados asociados a distintas zonas tropicales, con altos niveles de divergencia intraespecífica en algunos taxones. Esta información sugiere una historia evolutiva influenciada por procesos de aislamiento geográfico y diversificación ecológica. El estudio contribuye a la comprensión filogenética del género Psychotria y resalta la utilidad de los marcadores cloroplásticos como herramientas para evaluar la diversidad genética y la relación evolutiva entre especies tropicales de Rubiaceae.
Para realizar este proyecto se siguió estos pasos:

## 1. Selección y descarga
Se buscó en Genbak  organism[ORGN]="Psychotria" AND rbcL[gene], se seleccionó 26 epsecies asegurandóse que tengan una distribucción tropical y se descargó todas en un sólo archivo en formato FASTA.


## Descarga de las secuencias

![App Screenshot](Descargar%20secuencias%20en%20formato%20FASTA.jpg)

##  Anexo A — Archivo único de secuencias de la Familia *Psychotria* sin curar

El archivo FASTA con las secuencias obtenidas de GenBank se encuentra disponible aquí:

[📄 Descargar ANEXO A (FASTA)](ANEXO%20A.fasta)



## 2. Control de calidad y curación
Se verificó la longitud y calidad de las secuencias obtenidas, eliminando aquellas que presentaban ambigüedades, regiones incompletas o fragmentos parciales que pudieran comprometer la precisión del alineamiento. En los casos en que se detectaron secuencias duplicadas, se conservó únicamente una muestra representativa por localidad o espécimen, con el fin de evitar redundancias y mantener la representatividad biogeográfica del conjunto de datos.

## Curación manual de datos en MEGA 11
![App Screenshot](Curacion%20manual%20del%20Anexo%20A.jpg)

El archivo FAST con las secuencias obtenidas tras curar manualmente se encuentra disponible aquí:
[📄 Descargar Secuencias Curadas manualmente (FASTA)](Secuencias%20Curadas%20manualmente.fas)

## 3. Alineamiento
Para el alineamiento de las secuencias curadas se utilizará MAFFT, un programa de alineamiento múltiple de secuencias que permite organizar nucleótidos homólogos de manera precisa y eficiente. El archivo FASTA previamente curado en MEGA será ingresado a MAFFT utilizando parámetros automáticos, lo que generará un alineamiento global considerando homología entre todas las secuencias.
## Cargar el archivo Secuencias Curadas manualmente en MAFFT
![App Screenshot](Cargar%20el%20archivo.jpg)

## Parámetros de entrada y formato para alineamiento de secuencias
![App Screenshot](Datos%20de%20entrada.jpg)
Tipo de secuencias (MAYÚSCULAS / minúsculas): Aminoácido → MAYÚSCULAS; Nucleótido → minúsculas

**Nota:** Todas las secuencias de ADN como rbcL se ingresarán en minúsculas, para mantener consistencia y facilitar la lectura de MAFFT.

Dirección de las secuencias de nucleótidos: Ajustar la dirección según la primera secuencia

**Nota:** Esto asegura que todas las secuencias estén orientadas de manera consistente respecto a la primera secuencia, evitando posibles inversiones que afectarían el alineamiento. Es suficientemente preciso para secuencias del mismo marcador.

Orden de salida: Alineado

**Nota:** Las secuencias en el archivo de salida se ordenarán en el mismo orden que el alineamiento, facilitando la visualización y posteriores análisis filogenéticos.

Longitud del título en formato Clustal: 10

**Nota:** Solo se usa la primera palabra de cada título como identificador. Esto permite un formato legible y compatible con programas que leen Clustal, sin truncar información crítica de los IDs de GenBank.

Nombre del trabajo: Alineamiento final

**Nota:** Nombre descriptivo para identificar el archivo de salida, este campo es opcional

## Configuración avanzada
### Configuración automática

![App Screenshot](configuracion%20avanzada.jpg)

- Configuración avanzada: se seleccionó “Automático” porque MAFFT elige la estrategia óptima según el número de secuencias y el tamaño del dataset, equilibrando velocidad y precisión.

### Método de alineamiento
![App Screenshot](Segmentos%20no%20relacionados.jpg)

- Método de alineamiento: se eligió "Intenta alinear las regiones con huecos de todos modos” porque algunas secuencias presentan insertos o deleciones largas y se busca mejorar la homología en regiones con huecos.

### Parámetros
![App Screenshot](Otros%20parametros.jpg)

- Matriz de puntuación (BLOSUM62 / 200PAM κ=2) se eligió por ser la predeterminada estándar, adecuada para proteínas y ADN divergente respectivamente, asegurando una alineación confiable.

- Penalización por apertura de hueco (1.53): se dejó por defecto para equilibrar la introducción de huecos sin sobre-penalizar regiones con insertos.

- Valor de desplazamiento (0.0): se mantuvo predeterminado para evitar movimientos locales innecesarios que compliquen la alineación.

- Tratamiento de N en nucleótidos (cero): se escogió para que las bases desconocidas no afecten la puntuación de alineación.

Árbol guía (UPGMA):se dejó por defecto, ya que proporciona un orden inicial eficiente para el alineamiento progresivo.
### Homólogos de Mafft
![App Screenshot](Homológos.jpg)

- Homólogos de MAFFT (desactivado) porque solo se requiere alinear las secuencias de entrada sin incorporar secuencias externas.

- Gráficos de resultados (secuencia superior frente a las demás, trazado y alineación) se seleccionaron para facilitar la visualización de la alineación y de regiones problemáticas en el dataset de ADN.

Una vez se obtenga en MFFT versión 7 el alineamiento final, se exportó el alineamiento final en FASTA.
El archivo FAST con las secuencias alineadas se encuentra disponible aquí:
[📄 Descargar ANEXO B.1(FASTA)](ANEXO%20B%20.%201.fasta)

 Por otro lado, para convertir de archivo FASTA a Phylip se utilizó el siguiente Scrpt en R:
 
### Script R: FASTA -> PHYLIP


#### Rutas (ajustadas al nombre correcto del archivo)
ruta_fasta <- "C:\\Users\\USER\\Downloads\\PROYECTO DE BIOTECNOLOGÍA VEGETAL\\ANEXO B.1.fas"
ruta_phylip <- "C:\\Users\\USER\\Downloads\\PROYECTO DE BIOTECNOLOGÍA VEGETAL\\ANEXO_B1.phy"

#### Instalar paquetes 
if (!requireNamespace("seqinr", quietly = TRUE)) install.packages("seqinr")
if (!requireNamespace("ape", quietly = TRUE)) install.packages("ape")

#### Cargar librerías
library(seqinr)
library(ape)

#### Leer archivo FASTA con seqinr
seqs_list <- seqinr::read.fasta(file = ruta_fasta, seqtype = "DNA", as.string = FALSE, forceDNAtolower = FALSE)

#### Verificar que se hayan leído secuencias
if (length(seqs_list) == 0) stop("No se leyó ninguna secuencia. Verifica la ruta o el formato del archivo.")

#### Verificar longitudes iguales
lengths <- sapply(seqs_list, length)
if (length(unique(lengths)) != 1) {
  stop("ERROR: No todas las secuencias tienen la misma longitud. Longitudes encontradas:\n",
       paste(names(lengths), lengths, sep = ": ", collapse = "; "))
}

#### Convertir a matriz y luego a formato DNAbin
seq_matrix <- do.call(rbind, lapply(seqs_list, function(v) toupper(as.character(v))))
rownames(seq_matrix) <- names(seqs_list)
dna_bin <- ape::as.DNAbin(seq_matrix)

#### Exportar a formato PHYLIP
ape::write.dna(dna_bin, file = ruta_phylip, format = "sequential", nbcol = -1, colsep = " ")

cat("Conversión completada correctamente.\nArchivo PHYLIP guardado en:\n", ruta_phylip, "\n")

El archivo PHY con las secuencias alineadas se encuentra disponible aquí:
[📄 Descargar ANEXO B.1(FASTA)](ANEXO%20B%20.%202.phy) 
## 4.Análisis filogenético 

Se estimó las distancias genéticas (p-distance ) con MEGA  11 y se exportó las matrices en Excel

#### Estimación de distancias genéticas en MEGA 11

![App Screenshot](calculo%20de%20distancia.jpg)

La matriz de las distancias genéticas se encuentra disponible aquí:
[📄 Descargar ANEXOC (xlxs)](ANEXO%20C.xlsx)

### Creación del árbol filogenético

Se construyó un árbol filogenético con MEGA 11:  NJ con Bootstrap y se guardó el árbol en Newick.

![App Screenshot](metodo%20bootsrap.jpg)

Para construir el arból filógenetico es importante guardar el ANEXO B.1(fasta) en formato MEGA, se lo abre con MEGA 11 y se va a la opción de Analysis, después a Phylogeny opción Construct/Test ML o NJ y se abre una interfaz como la que se muestra en la figura de arriba, finalmemnte se modifica la parte de test phylogeny y se coloca el método bootstrao >1000 secuencias como se observa en la captura de imagén y el programa dará un árbol filogenético que posteriormente se descargará en forfamo Newick.

El árbol filogenético se encuentra disponible aquí:
[📄 Descargar Arbol filogenético (xlxs)](ARBOL%20NJ.pgn)
## 5. Análisis poblacional / estadística
Se realizó un análisis de frecuencia de haplotipos, diversidad haplotípica y diversidad nucleótidica en Rstudio. Posteriormente se realizó un análisis PCoA/PCA sobre matriz de distancias genéticas en R studio utilizando los paquetes vegan y ade4, un clustering (UPGMA/ward), y AMOVA para evaluar estructura entre grupos geográficos utilizando los paquetes Arlequin o poppr y finalmente se calculó soportes estadísticos p-values y ΦST 
Para el aálisis denético se usó el siguiente Script

### A. ANÁLISIS GENÉTICO: HAPLOTIPOS, Hd Y π CON CORRECCIÓN DE NOMBRES

if(!require(ape)) install.packages("ape")
if(!require(pegas)) install.packages("pegas")

library(ape)
library(pegas)


##### 1. Leer archivo FASTA y limpiar nombres

ruta <- "C:/Users/USER/Downloads/PROYECTO DE BIOTECNOLOGÍA VEGETAL/ANEXO B.1.fas"

alignment <- read.dna(ruta, format = "fasta")

##### Limpiar nombres de secuencias 
rownames(alignment) <- gsub(" ", "_", rownames(alignment))
rownames(alignment) <- gsub("[^A-Za-z0-9_]", "", rownames(alignment))

##### Verificar lectura correcta
cat("Secuencias cargadas correctamente:", nrow(alignment), "secuencias de", ncol(alignment), "bp.\n\n")


##### 2. Identificar haplotipos

haps <- haplotype(alignment)


##### 3. Calcular frecuencias de haplotipos

frecuencias <- haploFreq(haps)


##### 4. Calcular diversidad haplotípica (Hd) y nucleotídica (π)

Hd <- hap.div(alignment)
Pi <- nuc.div(alignment)


##### 5. Crear tabla resumen

tabla_resumen <- data.frame(
  Numero_de_Secuencias = nrow(alignment),
  Numero_de_Haplotipos = length(haps),
  Diversidad_Haplotipica_Hd = round(Hd, 4),
  Diversidad_Nucleotidica_Pi = round(Pi, 4)
)


##### 6. Mostrar resultados

cat("RESULTADOS DEL ANÁLISIS GENÉTICO\n")
print(tabla_resumen)
cat("\nFrecuencia de haplotipos:\n")
print(frecuencias)

##### 7.Guardar tabla en CSV
write.csv(tabla_resumen,
          "C:/Users/USER/Downloads/PROYECTO DE BIOTECNOLOGÍA VEGETAL/Resumen_Haplotipos.csv",
          row.names = FALSE)
          
### B. PCOA BASADO EN DISTANCIAS


##### CARGAR LIBRERÍAS

library(readxl)
library(vegan)
library(ape)
library(poppr)
library(pegas)
library(calibrate)


##### LEER MATRIZ DE DISTANCIAS DESDE EXCEL

ruta <- "C:/Users/USER/Downloads/PROYECTO DE BIOTECNOLOGÍA VEGETAL/ANEXO C.xlsx"

##### Leer hoja 1 
dist_data <- read_excel(ruta, sheet = 1)

##### Si la primera columna no es numérica, se toma como nombres de muestra
if (!is.numeric(dist_data[[1]])) {
  dist_data <- as.data.frame(dist_data)   # convertir a data.frame
  rownames(dist_data) <- dist_data[[1]]   # usar primera columna como nombres
  dist_data <- dist_data[, -1]   }

##### Convertir el resto a numérico
dist_matrix <- as.matrix(sapply(dist_data, as.numeric))


##### Asegurar que filas y columnas tengan los mismos nombres
rownames(dist_matrix) <- rownames(dist_data)
colnames(dist_matrix) <- rownames(dist_data)

##### Verificar que la matriz sea cuadrada
if (nrow(dist_matrix) != ncol(dist_matrix)) {
  stop("⚠ La matriz no es cuadrada. Revisa tu archivo Excel.")
}

##### Convertir a objeto de distancia
dist_matrix <- as.dist(dist_matrix)


#####  ANÁLISIS DE COORDENADAS PRINCIPALES (PCoA)

pcoa_result <- cmdscale(dist_matrix, k = 2, eig = TRUE)

##### Mostrar coordenadas de las muestras
cat("\n=== COORDENADAS DE LAS MUESTRAS ===\n")
print(round(pcoa_result$points, 4))

##### Calcular porcentaje de varianza explicada
var_exp <- round((pcoa_result$eig / sum(pcoa_result$eig)) * 100, 2)
cat("\n=== VARIANZA EXPLICADA (%) ===\n")
print(var_exp[1:23])


##### GRAFICAR PCoA 

labels_cortos <- substr(rownames(pcoa_result$points), 1, 10)
colores <- rainbow(nrow(pcoa_result$points))

##### Abre una nueva ventana de gráficos 
if (dev.cur() == 1) windows()  # usa quartz() en Mac
windows()  
##### Graficar PCoA
plot(pcoa_result$points,
     pch = 19, col = colores,
     xlab = paste0("Eje 1 (", var_exp[1], "%)"),
     ylab = paste0("Eje 2 (", var_exp[2], "%)"),
     main = "PCoA basado en matriz de distancias genéticas")
### C.  CLUSTERING GENÉTICO (UPGMA y WARD) 

#####  Cargar librerías
library(readxl)
library(vegan)
library(cluster)
library(dendextend)

#####  Ruta del archivo
ruta <- "C:/Users/USER/Downloads/PROYECTO DE BIOTECNOLOGÍA VEGETAL/ANEXO C.xlsx"

#####  Leer la hoja 1 (ajusta si es otra)
datos <- read_excel(ruta, sheet = 1)

##### Revisar los nombres de las columnas
cat("\n=== NOMBRES DE COLUMNAS ===\n")
print(names(datos))

##### Si la primera columna son los nombres de las muestras, se usa como rownames
if (!is.numeric(dist_data[[1]])) {
  dist_data <- as.data.frame(dist_data)   # convertir a data.frame
  rownames(dist_data) <- dist_data[[1]]   # usar primera columna como nombres
  dist_data <- dist_data[, -1]   }


##### Convertir todo a numérico (reemplazando texto o celdas vacías)
datos_num <- as.data.frame(sapply(datos, as.numeric))
rownames(datos_num) <- rownames(datos)

##### Eliminar filas/columnas vacías
datos_num <- datos_num[complete.cases(datos_num), ]
datos_num <- datos_num[, colSums(is.na(datos_num)) == 0]

##### Confirmar estructura final
cat("\n=== MATRIZ FINAL SIN NA ===\n")
print(dim(datos_num))


#####  Calcular matriz de distancias genéticas

dist_matrix <- vegdist(datos_num, method = "euclidean")

##### Verificar si hay valores infinitos o NA
if (any(is.na(dist_matrix))) stop("Hay NA en la matriz de distancias. Revisa tu archivo Excel.")

hc_upgma <- hclust(dist_matrix, method = "average")
plot(hc_upgma, main = ".", xlab = "", sub = "")

hc_ward <- hclust(dist_matrix, method = "ward.D2")
plot(hc_ward, main = "Clustering Ward (matriz de distancias)", xlab = "", sub = "")
##### Aumentar el área del gráfico antes de graficar
par(mar = c(10, 4, 4, 2))  # más espacio inferior

plot(hc_upgma, 
     main = ".", 
     xlab = "", sub = "",
     cex = 0.8, hang = -1, las = 2)
 ### D. AMOVA P-VALUE Y ΦST
 #### Cargar librerías
library(ape)
library(poppr)
library(pegas)
library(ade4)

####  Cargar el alineamiento FASTA

ruta_fasta <- "C:/Users/USER/Downloads/PROYECTO DE BIOTECNOLOGÍA VEGETAL/ANEXO B.1.fas"

alignment <- read.dna(ruta_fasta, format = "fasta")


#### Crear tabla de metadatos 

metadata <- data.frame(
  id = names(alignment),
  nombre = c(
    "Psychotria homalosperma",
    "Psychotria viridiflora",
    "Psychotria limba",
    "Psychotria longituba",
    "Psychotria michelii",
    "Psychotria myriantha",
    "Psychotria rufofils",
    "Psychotria subobliqua",
    "Psychotria carthagenensis",
    "Psychotria hoffmannseggiana",
    "Psychotria ligustrifolia",
    "Psychotria poeppigiana_1",
    "Psychotria poeppigiana_2",
    "Psychotria kirkii",
    "Psychotria colorata",
    "Psychotria tenuifolia_1",
    "Psychotria tenuifolia_2",
    "Psychotria lundellii",
    "Psychotria mapourioides",
    "Psychotria trichotoma",
    "Psychotria tucheri",
    "Psychotria sepensis",
    "Psychotria asiatica"
  ),
  origen = c(
    "Asia", "Asia", "África", "África", "América", "América", "América", "América",
    "América", "América", "América", "América", "América", "África", "América",
    "América", "América", "América", "América", "América", "África", "Asia", "Asia"
  )
)

#### Verificar estructura
print(metadata)


####  Alinear nombres entre FASTA y metadatos

#### Asegurar que las secuencias coincidan con los IDs del metadata
alignment <- alignment[names(alignment) %in% metadata$id]
metadata <- metadata[metadata$id %in% names(alignment), ]


#### Convertir a objeto genético

genind_obj <- DNAbin2genind(alignment)
pop(genind_obj) <- as.factor(metadata$origen)


####  Análisis AMOVA

amova_result <- poppr.amova(genind_obj, ~origen)
print(amova_result)


#### Test de permutaciones

set.seed(123)
amova_test <- randtest(amova_result, nrepet = 999)
print(amova_test)
#### Revisar nombres disponibles en el resultado
cat("\nEstructura del objeto AMOVA:\n")
print(names(amova_result))

#### Intentar extraer ΦST y p-value según formato
phi_st <- NA
p_value <- NA

if ("statphi" %in% names(amova_result)) {
  phi_st <- amova_result$statphi
}
if ("pvalue" %in% names(amova_result)) {
  p_value <- amova_result$pvalue
}

#### Si no existen, buscar en sublistas
if (is.list(amova_result$tab)) {
  if ("Phi.ST" %in% colnames(amova_result$tab)) {
    phi_st <- amova_result$tab["Among groups", "Phi.ST"]
  }
}


#### Imprimir resultados


if (!is.na(phi_st)) {
  cat("ΦST =", round(phi_st, 4), "\n")
} else {
  cat("ΦST no disponible en el objeto.\n")
}

if (!is.na(p_value)) {
  cat("p-value =", round(p_value, 4), "\n")
} else {
  cat("p-value no disponible en el objeto.\n")
}

cat("============================\n")
### E. VISUALIZACIONES
library(ape)
library(seqinr)

##### Leer alineamiento
NUEVO <- "C:\\Users\\USER\\Downloads\\PROYECTO DE BIOTECNOLOGÍA VEGETAL\\ANEXO x fas"
alignment <- read.dna("ANEXO x fas", format = "fasta")



##### Mostrar nombres originales
cat("Nombres originales:\n")
print(rownames(alignment))

rownames(alignment) <- sapply(strsplit(rownames(alignment), "_"), `[`, 1)
rownames(alignment) <- substr(rownames(alignment), 1, 11)
##### Verifica los nuevos nombres
cat("\nNombres modificados (solo código):\n")
print(rownames(alignment))

##### Graficar alineamiento 
par(mar = c(2, 10, 3, 1)) 
image.DNAbin(
  alignment[, 1:60],
  cex.lab = 0.8,
  cex.axis = 0.8
)
#### MATRIZ DE DISTANCIAS GENÉTICAS
library(ape)
library(pegas)
library(adegenet)
library(poppr)
library(ggplot2)
library(reshape2)
library(igraph)

##### Calcular matriz de distancias genéticas
dist_matrix <- dist.dna(alignment, model = "K80")

##### Convertir a formato largo
dist_df <- as.matrix(dist_matrix)
heat_df <- melt(dist_df)

##### Graficar heatmap con texto en negrita y mayor tamaño
ggplot(heat_df, aes(Var1, Var2, fill = value)) +
  geom_tile() +
  scale_fill_gradient(low = "white", high = "purple") +
  theme_minimal() +
  theme(
    axis.text.x = element_text(angle = 90, vjust = 0.5, hjust = 1,
                               face = "bold", size = 10),
    axis.text.y = element_text(face = "bold", size = 10)
  ) +
  labs(title = "Matriz de distancias genéticas", fill = "Distancia")
  
### RED DE HAPLOTIPOS
haps <- haplotype(alignment)
net <- haploNet(haps)

##### Graficar la red de haplotipos
plot(net, size = attr(net, "freq"), scale.ratio = 0.5,
     main = "Red de haplotipos (pegas)")
legend("topright", legend = "Cada nodo = haplotipo",
       bty = "n")












