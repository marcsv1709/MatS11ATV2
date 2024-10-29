# Exploração das Bissetrizes Interna e Externa em Triângulos

---

## Parte A – Bissetriz Interna

### Teorema da Bissetriz Interna

**Hipótese:** No triângulo \( ABC \), a bissetriz interna do ângulo em \( A \) intersecta o lado \( BC \) no ponto \( D \).

**Tese:** A bissetriz interna divide o lado \( BC \) em segmentos proporcionais aos lados adjacentes:
\[
\frac{BD}{DC} = \frac{AB}{AC}
\]

### Implementação em Python

```python
def bissetriz(a, b, c, tipo='interna'):
    """
    Calcula as divisões do lado BC pela bissetriz interna ou externa do ângulo em A.

    Parâmetros:
    a (float): comprimento do lado BC
    b (float): comprimento do lado AC
    c (float): comprimento do lado AB
    tipo (str): 'interna' para bissetriz interna ou 'externa' para bissetriz externa

    Retorna:
    tuple: (BD, DC) os segmentos em que o lado BC é dividido
    """
    if tipo == 'interna':
        # Bissetriz interna
        BD = (c / (b + c)) * a
        DC = (b / (b + c)) * a
        return BD, DC
    elif tipo == 'externa':
        # Verifica se c != b para evitar divisão por zero
        if c == b:
            raise ValueError("Para a bissetriz externa, os lados AB e AC não podem ser iguais.")
        # Bissetriz externa
        DC = (b * a) / (c - b)
        BD = a + DC  # D está fora do segmento BC
        return BD, DC
    else:
        raise ValueError("Tipo inválido. Escolha 'interna' ou 'externa'.")

# Exemplo de uso
a = float(input("Digite o comprimento do lado a (BC): "))
b = float(input("Digite o comprimento do lado b (AC): "))
c = float(input("Digite o comprimento do lado c (AB): "))
tipo = input("Digite o tipo de bissetriz ('interna' ou 'externa'): ").strip().lower()

try:
    BD, DC = bissetriz(a, b, c, tipo)
    print(f"\nA bissetriz {tipo} divide o lado BC em:")
    print(f"BD = {BD:.2f}")
    print(f"DC = {DC:.2f}")
    print(f"\nVerificando a proporcionalidade:")
    razao_BD_DC = BD / DC
    razao_AB_AC = c / b
    print(f"Razão BD/DC = {razao_BD_DC:.2f}")
    print(f"Razão AB/AC = {razao_AB_AC:.2f}")
except ValueError as e:
    print(f"Erro: {e}")

