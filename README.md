<!DOCTYPE html>
<html lang="ar">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>متجري</title>
  <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css">
  <script src="https://unpkg.com/react@17/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
  <script src="https://kit.fontawesome.com/a076d05399.js" crossorigin="anonymous"></script>
  <style>
    body {
      direction: rtl;
      text-align: right;
      background-image: url('https://img.freepik.com/premium-photo/abstract-blue-background-with-smooth-lines_476363-511.jpg?size=626&ext=jpg/1200x800'); /* تغيير الرابط إلى صورة الخلفية المرغوبة */
      background-size: cover;
      background-attachment: fixed;
    }
    .card {
      background: rgba(255, 255, 255, 0.8);
    }
    .navbar, .btn, .list-group-item {
      background: rgba(255, 255, 255, 0.9);
    }
  </style>
</head>
<body>
  <div id="root"></div>

  <script type="text/babel">
    const { useState, useEffect } = React;

    const products = [
      {
        id: 1,
        name: 'لابتوب',
        description: 'لابتوب عالي الجودة بأداء ممتاز.',
        price: 1000,
        rating: 4.5,
        category: 'electronics',
        image: 'https://th.bing.com/th/id/OIP.17vy8YBnfQ4tSrdQ7nOXtAHaEK?rs=1&pid=ImgDetMain/150',
      },
      {
        id: 2,
        name: 'هاتف ذكي',
        description: 'هاتف ذكي عالي الجودة بأداء ممتاز.',
        price: 1000,
        rating: 4.5,
        category: 'electronics',
        image: 'data:image/jpeg;base64,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',
      },
      {
        id: 3,
        name: 'قميص',
        description: 'قميص عصري بألوان متنوعة.',
        price: 50,
        rating: 4.0,
        category: 'clothing',
        image: 'https://www.bing.com/th?id=OIP.njTGNxMOkJAbunGYgtmjswHaJo&w=150&h=195&c=8&rs=1&qlt=90&o=6&pid=3.1&rm=2/150',
      },
      {
        id: 4,
        name: 'كتاب',
        description: 'كتاب ممتع ومفيد للقراءة.',
        price: 20,
        rating: 5.0,
        category: 'books',
        image: 'https://th.bing.com/th/id/OIP.ylU6kF63QLl317sPhJiLnwHaHa?w=198&h=198&c=7&r=0&o=5&pid=1.7/150',
      },
      {
        id: 5,
        name: 'ساعة يدوية',
        description: 'ساعة رجالية رائعة',
        price: 20,
        rating: 5.0,
        category: 'clothing',
        image: 'data:image/jpeg;base64,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',
      },
    ];

    function App() {
      const [cart, setCart] = useState([]);
      const [favorites, setFavorites] = useState([]);
      const [selectedProduct, setSelectedProduct] = useState(null);

      useEffect(() => {
        const storedCart = JSON.parse(localStorage.getItem('cart')) || [];
        const storedFavorites = JSON.parse(localStorage.getItem('favorites')) || [];
        setCart(storedCart);
        setFavorites(storedFavorites);
      }, []);

      useEffect(() => {
        localStorage.setItem('cart', JSON.stringify(cart));
        localStorage.setItem('favorites', JSON.stringify(favorites));
      }, [cart, favorites]);

      const handleAddToCart = (product) => {
        setCart([...cart, product]);
      };

      const handleRemoveFromCart = (productId) => {
        setCart(cart.filter((item) => item.id !== productId));
      };

      const handleAddToFavorites = (product) => {
        setFavorites([...favorites, product]);
      };

      const handleRemoveFromFavorites = (productId) => {
        setFavorites(favorites.filter((item) => item.id !== productId));
      };

      const handleShowProductDetails = (product) => {
        setSelectedProduct(product);
      };

      const handleCheckout = () => {
        const phoneNumber = '212684841429'; // رقم الواتساب الخاص بك
        const cartContent = cart.map((item) => `${item.name}:\n${item.image}\n$${item.price.toFixed(2)}`).join('\n\n');
        const totalAmount = cart.reduce((total, product) => total + product.price, 0).toFixed(2);
        const message = `مرحبًا، أود شراء المنتجات التالية:\n\n${cartContent}\nالمجموع: $${totalAmount}`;
        const encodedMessage = encodeURIComponent(message);
        const whatsappURL = `https://wa.me/${phoneNumber}?text=${encodedMessage}`;

        window.open(whatsappURL, '_blank');
        setCart([]);
      };

      return (
        <div className="container">
          <nav className="navbar navbar-expand-lg navbar-dark bg-success mb-4">
            <div className="container-fluid">
              <a className="navbar-brand" href="#">
                متجري
              </a>
              <button
                className="navbar-toggler"
                type="button"
                data-bs-toggle="collapse"
                data-bs-target="#navbarNav"
                aria-controls="navbarNav"
                aria-expanded="false"
                aria-label="Toggle navigation"
              >
                <span className="navbar-toggler-icon"></span>
              </button>
              <div className="collapse navbar-collapse" id="navbarNav">
                <ul className="navbar-nav me-auto">
                  <li className="nav-item">
                    <a className="nav-link" href="#" onClick={() => setSelectedProduct(null)}>
                      المنتجات
                    </a>
                  </li>
                </ul>
                <ul className="navbar-nav">
                  <li className="nav-item">
                    <a className="nav-link" href="#" onClick={() => setSelectedProduct(null)}>
                      <i className="fas fa-heart"></i> المفضلة ({favorites.length})
                    </a>
                  </li>
                  <li className="nav-item">
                    <a className="nav-link" href="#" onClick={() => setSelectedProduct(null)}>
                      <i className="fas fa-shopping-cart"></i> السلة ({cart.length})
                    </a>
                  </li>
                </ul>
              </div>
            </div>
          </nav>

          {!selectedProduct ? (
            <>
              <ProductList products={products} onAddToCart={handleAddToCart} onAddToFavorites={handleAddToFavorites} onShowDetails={handleShowProductDetails} />
              <Cart cart={cart} onRemoveFromCart={handleRemoveFromCart} onCheckout={handleCheckout} />
              <Favorites favorites={favorites} onRemoveFromFavorites={handleRemoveFromFavorites} onAddToCart={handleAddToCart} />
            </>
          ) : (
            <ProductDetails product={selectedProduct} onAddToCart={handleAddToCart} onAddToFavorites={handleAddToFavorites} onClose={() => setSelectedProduct(null)} />
          )}

          <Checkout onCheckout={handleCheckout} />
        </div>
      );
    }

    function ProductList({ products, onAddToCart, onAddToFavorites, onShowDetails }) {
      const [categoryFilter, setCategoryFilter] = useState('');
      const [searchQuery, setSearchQuery] = useState('');

      const handleCategoryFilter = (category) => {
        setCategoryFilter(category);
      };

      const handleSearch = (e) => {
        setSearchQuery(e.target.value.toLowerCase());
      };

      const filteredProducts = products.filter(
        (product) =>
          (categoryFilter === '' || product.category === categoryFilter) &&
          product.name.toLowerCase().includes(searchQuery)
      );

      return (
        <div>
          <div className="mb-3">
            <div className="btn-group">
              <button className={`btn btn-outline-success ${categoryFilter === '' ? 'active' : ''}`} onClick={() => handleCategoryFilter('')}>
                الكل
              </button>
              <button className={`btn btn-outline-success ${categoryFilter === 'electronics' ? 'active' : ''}`} onClick={() => handleCategoryFilter('electronics')}>
                الكترونيات
              </button>
              <button className={`btn btn-outline-success ${categoryFilter === 'clothing' ? 'active' : ''}`} onClick={() => handleCategoryFilter('clothing')}>
                ملابس
              </button>
              <button className={`btn btn-outline-success ${categoryFilter === 'books' ? 'active' : ''}`} onClick={() => handleCategoryFilter('books')}>
                كتب
              </button>
            </div>
          </div>
          <div className="input-group mb-3">
            <input type="text" className="form-control" placeholder="ابحث عن منتج" value={searchQuery} onChange={handleSearch} />
            <button className="btn btn-outline-success" type="button" onClick={() => setSearchQuery('')}>
              <i className="fas fa-times"></i>
            </button>
          </div>
          <div className="row row-cols-1 row-cols-md-3 g-4">
            {filteredProducts.map((product) => (
              <div key={product.id} className="col">
                <div className="card h-100">
                  <img src={product.image} className="card-img-top" alt={product.name} />
                  <div className="card-body">
                    <h5 className="card-title">{product.name}</h5>
                    <Rating value={product.rating} />
                    <p className="card-text">{product.description}</p>
                    <h6 className="card-subtitle mb-2 text-muted">${product.price.toFixed(2)}</h6>
                    <div className="d-flex justify-content-between align-items-center">
                      <button className="btn btn-outline-success" onClick={() => onAddToCart(product)}>
                        <i className="fas fa-shopping-cart me-2"></i>
                        إضافة إلى السلة
                      </button>
                      <button className="btn btn-outline-danger" onClick={() => onAddToFavorites(product)}>
                        <i className="fas fa-heart me-2"></i>
                        المفضلة
                      </button>
                    </div>
                    <button className="btn btn-outline-secondary mt-3" onClick={() => onShowDetails(product)}>
                      <i className="fas fa-info-circle me-2"></i>
                      عرض التفاصيل
                    </button>
                  </div>
                </div>
              </div>
            ))}
          </div>
        </div>
      );
    }

    function Cart({ cart, onRemoveFromCart, onCheckout }) {
      const calculateTotal = () => {
        return cart.reduce((total, product) => total + product.price, 0);
      };

      return (
        <div className="mt-4">
          <h4>سلة التسوق</h4>
          {cart.length === 0 ? (
            <p>لا توجد منتجات في السلة.</p>
          ) : (
            <ul className="list-group">
              {cart.map((product) => (
                <li key={product.id} className="list-group-item d-flex justify-content-between align-items-center">
                  {product.name}
                  <div>
                    <button className="btn btn-sm btn-outline-danger" onClick={() => onRemoveFromCart(product.id)}>
                      <i className="fas fa-times"></i>
                    </button>
                  </div>
                </li>
              ))}
            </ul>
          )}
          {cart.length > 0 && (
            <div className="mt-3">
              <h5>المجموع: ${calculateTotal().toFixed(2)}</h5>
              <button className="btn btn-success" onClick={onCheckout}>
                <i className="fab fa-whatsapp me-2"></i>
                إتمام الشراء عبر واتساب
              </button>
            </div>
          )}
        </div>
      );
    }

    function Favorites({ favorites, onRemoveFromFavorites, onAddToCart }) {
      return (
        <div className="mt-4">
          <h4>المفضلة</h4>
          {favorites.length === 0 ? (
            <p>لا توجد منتجات في المفضلة.</p>
          ) : (
            <ul className="list-group">
              {favorites.map((product) => (
                <li key={product.id} className="list-group-item d-flex justify-content-between align-items-center">
                  {product.name}
                  <div>
                    <button className="btn btn-sm btn-outline-success me-2" onClick={() => onAddToCart(product)}>
                      <i className="fas fa-shopping-cart"></i>
                    </button>
                    <button className="btn btn-sm btn-outline-danger" onClick={() => onRemoveFromFavorites(product.id)}>
                      <i className="fas fa-times"></i>
                    </button>
                  </div>
                </li>
              ))}
            </ul>
          )}
        </div>
      );
    }

    function ProductDetails({ product, onAddToCart, onAddToFavorites, onClose }) {
      return (
        <div className="card mb-4">
          <img src={product.image} className="card-img-top" alt={product.name} />
          <div className="card-body">
            <h5 className="card-title">{product.name}</h5>
            <Rating value={product.rating} />
            <p className="card-text">{product.description}</p>
            <h6 className="card-subtitle mb-2 text-muted">${product.price.toFixed(2)}</h6>
            <div className="d-flex justify-content-between align-items-center">
              <button className="btn btn-outline-success" onClick={() => onAddToCart(product)}>
                <i className="fas fa-shopping-cart me-2"></i>
                إضافة إلى السلة
              </button>
              <button className="btn btn-outline-danger" onClick={() => onAddToFavorites(product)}>
                <i className="fas fa-heart me-2"></i>
                المفضلة
              </button>
            </div>
            <button className="btn btn-outline-secondary mt-3" onClick={onClose}>
              <i className="fas fa-arrow-left me-2"></i>
              العودة
            </button>
          </div>
        </div>
      );
    }

    function Checkout({ onCheckout }) {
      return (
        <div className="mt-4">
          <h4>إتمام الشراء</h4>
          <button className="btn btn-success" onClick={onCheckout}>
            <i className="fab fa-whatsapp me-2"></i>
            الدفع عن طريق واتساب
          </button>
        </div>
      );
    }

    function Rating({ value }) {
      const stars = [];
      for (let i = 1; i <= 5; i++) {
        stars.push(
          <i key={i} className={`fas fa-star ${i <= value ? 'text-warning' : 'text-muted'}`}></i>
        );
      }
      return <div>{stars}</div>;
    }

    ReactDOM.render(<App />, document.getElementById('root'));
  </script>
</body>
</html>
