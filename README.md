## Zadatak 1
Drugi i treci blok koda. Prvi ostaje isti
```python
# (a) kolicina informacije po simbolu
I_x1 = -log2(p_X[0])
I_x2 = -log2(p_X[1])
I_x3 = -log2(p_X[2])
I_x4 = -log2(p_X[3])
print("I(x1) =",I_x1, "[bit/simbol]")
print("I(x2) =",I_x2, "[bit/simbol]")
print("I(x3) =",I_x3, "[bit/simbol]")
print("I(x4) =",I_x4, "[bit/simbol]")
```
```python
# (b) kolicina informacije poruke
np.random.seed(sval+1)
message = np.random.choice(X_symbols, size = 5, p = p_X)
print("message: ", message)
I_message = -np.log2([p_X[X_symbols.index(symbol)] for symbol in message]).sum()
print("I(message) =", I_message, "[bit/poruka]")
```

## Zadatak 4
Drugi blok koda, ispod ove slike

![image](https://github.com/MarkoPekas/tininf/assets/45564032/e5db2d24-c4f8-472a-af66-d4888e2c6327)
```python
# Ukupan broj znakova u tekstu
total_chars = sum(char_counts)

# Izračunavanje vjerojatnosti za svaki znak
char_probs = [count / total_chars for count in char_counts]

# Izračunavanje srednjeg sadržaja informacije (entropije)
entropy = -sum([prob * log2(prob) for prob in char_probs if prob > 0])

print(entropy)
```

## Zadatak 5
Ispod papiga

![image](https://github.com/MarkoPekas/tininf/assets/45564032/a404c773-45a4-4f0f-a43a-4ab92e74b652)

```python
# pretvori sliku u niz
color_array = np.array(parrot)
gray_array = np.array(gray_parrot)

# transformiraj sliku tako da svi pikseli budu pohranjeni u jednodimenzionalnom nizu
shape = color_array.shape
color_array = color_array.reshape(1,shape[0]*shape[1],shape[2])
shape = gray_array.shape
gray_array = gray_array.reshape(1,shape[0]*shape[1])

# izračunaj skup jedinstvenih vrijednosti piksela i broj pojavljivanja pojedinog piksela
unique_col_px, col_px_counts = np.unique(color_array, return_counts = True, axis = 1)
unique_col_px = np.array([str(px) for px in unique_col_px[0,:]])
color_dict = dict(zip(unique_col_px,col_px_counts))
# print("Colored parrot pixel counts:", color_dict)
unique_gray_px, gray_px_counts = np.unique(gray_array, return_counts = True, axis = 1)
unique_gray_px = np.array([str(px) for px in unique_gray_px[0]])
gray_dict = dict(zip(unique_gray_px,gray_px_counts))
# print("Gray parrot pixel counts:", gray_dict)

# izracun gubitka informacije prilikom transformacije u crno-bijelu skalu
# Izračunavanje vjerojatnosti pojavljivanja svakog piksela u obojanoj slici
color_probs = {px: count / sum(color_dict.values()) for px, count in color_dict.items()}

# Izračunavanje vjerojatnosti pojavljivanja svakog piksela u crno-bijeloj slici
gray_probs = {px: count / sum(gray_dict.values()) for px, count in gray_dict.items()}

# Izračunavanje ukupne količine informacije za obojanu sliku
info_color = -sum([count * log2(prob) for px, (prob, count) in zip(color_probs.keys(), zip(color_probs.values(), color_dict.values()))])

# Izračunavanje ukupne količine informacije za crno-bijelu sliku
info_gray = -sum([count * log2(prob) for px, (prob, count) in zip(gray_probs.keys(), zip(gray_probs.values(), gray_dict.values()))])

# Gubitak informacije
info_loss = info_color - info_gray
print(info_loss)
```
