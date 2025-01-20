# reto_05
Create a package with all code of class Shape, this exersice should be conducted in two ways:
A unique module inside of package Shape
Individual modules that import Shape in inheritates from it.
# Se estructura el codigo de la siguiente forma
shape_package/
├── __init__.py          # Marca el directorio como paquete
├── shape.py             # Módulo único con la clase Shape y sus derivados
├── rectangle.py         # Módulo con la clase Rectangle que hereda de Shape
├── square.py            # Módulo con la clase Square que hereda de Rectangle
├── triangle.py          # Módulo con la clase Triangle que hereda de Shape
└── point.py             # Módulo con la clase Point

## Módulo único dentro del paquete (shape.py) ## Modulos Individuales
En este enfoque, todo el código estará dentro de un único archivo llamado shape.py.
```
shape_package/shape.py
```
```
# shape.py

class Point:
    def __init__(self, x: int, y: int):
        self._x = x
        self._y = y

    def get_x(self):
        return self._x

    def get_y(self):
        return self._y

    def compute_distance(self, other: 'Point') -> float:
        return ((self._x - other.get_x()) ** 2 + (self._y - other.get_y()) ** 2) ** 0.5


class Shape:
    def __init__(self):
        self._vertices = []
        self._edges = []
        self._inner_angles = []
        self._is_regular = False

    def get_vertices(self):
        return self._vertices

    def get_edges(self):
        return self._edges

    def get_inner_angles(self):
        return self._inner_angles

    def is_regular(self):
        return self._is_regular

    def compute_area(self):
        raise NotImplementedError("This method should be overridden in subclasses.")

    def compute_perimeter(self):
        raise NotImplementedError("This method should be overridden in subclasses.")

    def compute_inner_angles(self):
        raise NotImplementedError("This method should be overridden in subclasses.")


class Rectangle(Shape):
    def __init__(self, width: float, height: float):
        super().__init__()
        self._width = width
        self._height = height

    def get_width(self):
        return self._width

    def get_height(self):
        return self._height

    def compute_area(self) -> float:
        return self._width * self._height

    def compute_perimeter(self) -> float:
        return 2 * (self._width + self._height)


class Square(Rectangle):
    def __init__(self, side_length: float):
        super().__init__(side_length, side_length)


class Triangle(Shape):
    def __init__(self, point1: Point, point2: Point, point3: Point):
        super().__init__()
        self._vertices = [point1, point2, point3]
        self._edges = [Line(point1, point2), Line(point2, point3), Line(point3, point1)]
        self._inner_angles = self.compute_inner_angles()

    def compute_area(self) -> float:
        a = self._edges[0].get_length()
        b = self._edges[1].get_length()
        c = self._edges[2].get_length()
        s = (a + b + c) / 2
        return (s * (s - a) * (s - b) * (s - c)) ** 0.5

    def compute_perimeter(self) -> float:
        return sum(edge.get_length() for edge in self._edges)

    def compute_inner_angles(self) -> list:
        return [60.0, 60.0, 60.0]
```
## Módulos individuales que importan Shape y heredan de ella
En este enfoque, se separan las clases en archivos distintos, y cada módulo importa Shape para definir las clases derivadas.
```
shape_package/point.py
```
