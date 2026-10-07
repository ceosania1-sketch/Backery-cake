/* =====================================================
   AP SAIM BAKERY SHOP
   MAIN JAVASCRIPT
===================================================== */

document.addEventListener("DOMContentLoaded", () => {

    /* ================================================
       PRELOADER
    ================================================ */

    const preloader = document.getElementById("preloader");

    window.addEventListener("load", () => {

        setTimeout(() => {
            preloader.classList.add("hide");
        }, 900);

    });


    /* ================================================
       MOBILE MENU
    ================================================ */

    const menuBtn = document.getElementById("menuBtn");
    const mainNav = document.getElementById("mainNav");

    menuBtn.addEventListener("click", () => {

        mainNav.classList.toggle("open");

        const icon = menuBtn.querySelector("i");

        if (mainNav.classList.contains("open")) {
            icon.classList.remove("fa-bars");
            icon.classList.add("fa-xmark");
        } else {
            icon.classList.remove("fa-xmark");
            icon.classList.add("fa-bars");
        }

    });


    /* Close mobile menu after clicking */

    document.querySelectorAll("#mainNav a").forEach(link => {

        link.addEventListener("click", () => {
            mainNav.classList.remove("open");

            const icon = menuBtn.querySelector("i");

            icon.classList.remove("fa-xmark");
            icon.classList.add("fa-bars");
        });

    });


    /* ================================================
       SEARCH
    ================================================ */

    const searchBtn = document.getElementById("searchBtn");
    const searchPanel = document.getElementById("searchPanel");
    const closeSearch = document.getElementById("closeSearch");
    const searchInput = document.getElementById("searchInput");

    searchBtn.addEventListener("click", () => {

        searchPanel.classList.toggle("open");

        if (searchPanel.classList.contains("open")) {
            setTimeout(() => searchInput.focus(), 300);
        }

    });

    closeSearch.addEventListener("click", () => {
        searchPanel.classList.remove("open");
        searchInput.value = "";
        showAllProducts();
    });


    searchInput.addEventListener("input", () => {

        const query = searchInput.value.toLowerCase().trim();

        const products =
            document.querySelectorAll(".product-card");

        products.forEach(product => {

            const name =
                product.querySelector("h3")
                    .textContent
                    .toLowerCase();

            const description =
                product.querySelector("p")
                    .textContent
                    .toLowerCase();

            if (
                name.includes(query) ||
                description.includes(query)
            ) {
                product.classList.remove("hidden");
            } else {
                product.classList.add("hidden");
            }

        });

    });


    /* ================================================
       CATEGORY FILTER
    ================================================ */

    const filters =
        document.querySelectorAll(".filter");

    const categoryCards =
        document.querySelectorAll(".category-card");

    function filterProducts(category) {

        document.querySelectorAll(".product-card")
            .forEach(product => {

                if (
                    category === "all" ||
                    product.dataset.category === category
                ) {
                    product.classList.remove("hidden");
                } else {
                    product.classList.add("hidden");
                }

            });

    }


    filters.forEach(filter => {

        filter.addEventListener("click", () => {

            filters.forEach(btn =>
                btn.classList.remove("active")
            );

            filter.classList.add("active");

            const category =
                filter.dataset.category;

            filterProducts(category);

        });

    });


    categoryCards.forEach(card => {

        card.addEventListener("click", () => {

            categoryCards.forEach(item =>
                item.classList.remove("active")
            );

            card.classList.add("active");

            const category =
                card.dataset.category;

            filters.forEach(btn => {

                btn.classList.toggle(
                    "active",
                    btn.dataset.category === category
                );

            });

            filterProducts(category);

            document
                .getElementById("products")
                .scrollIntoView({
                    behavior: "smooth"
                });

        });

    });


    function showAllProducts() {

        document.querySelectorAll(".product-card")
            .forEach(product => {
                product.classList.remove("hidden");
            });

    }


    /* ================================================
       SORTING
    ================================================ */

    const sortProducts =
        document.getElementById("sortProducts");

    const productGrid =
        document.getElementById("productGrid");

    sortProducts.addEventListener("change", () => {

        const products =
            [...productGrid.querySelectorAll(".product-card")];

        const type = sortProducts.value;

        if (type === "low") {

            products.sort(
                (a,b) =>
                Number(a.dataset.price) -
                Number(b.dataset.price)
            );

        }

        if (type === "high") {

            products.sort(
                (a,b) =>
                Number(b.dataset.price) -
                Number(a.dataset.price)
            );

        }

        if (type === "rating") {

            products.sort(
                (a,b) =>
                Number(b.dataset.rating) -
                Number(a.dataset.rating)
            );

        }

        products.forEach(product =>
            productGrid.appendChild(product)
        );

    });


    /* ================================================
       CART
    ================================================ */

    let cart = [];

    const cartBtn =
        document.getElementById("cartBtn");

    const cartSidebar =
        document.getElementById("cartSidebar");

    const cartOverlay =
        document.getElementById("cartOverlay");

    const closeCart =
        document.getElementById("closeCart");

    const cartItems =
        document.getElementById("cartItems");

    const cartCount =
        document.getElementById("cartCount");

    const cartTotal =
        document.getElementById("cartTotal");


    function openCart() {

        cartSidebar.classList.add("open");
        cartOverlay.classList.add("show");

    }


    function closeCartSidebar() {

        cartSidebar.classList.remove("open");
        cartOverlay.classList.remove("show");

    }


    cartBtn.addEventListener(
        "click",
        openCart
    );

    closeCart.addEventListener(
        "click",
        closeCartSidebar
    );

    cartOverlay.addEventListener(
        "click",
        closeCartSidebar
    );


    /* Add products */

    document.querySelectorAll(".add-cart")
        .forEach(button => {

            button.addEventListener("click", () => {

                const product = {

                    name: button.dataset.name,

                    price: Number(
                        button.dataset.price
                    ),

                    image: button.dataset.image

                };


                const existing =
                    cart.find(
                        item =>
                        item.name === product.name
                    );


                if (existing) {

                    existing.quantity++;

                } else {

                    product.quantity = 1;

                    cart.push(product);

                }


                updateCart();

                showToast(
                    `${product.name} added to cart`
                );

                openCart();

            });

        });


    function updateCart() {

        cartItems.innerHTML = "";

        if (cart.length === 0) {

            cartItems.innerHTML = `

                <div class="empty-cart">

                    <i class="fa-solid fa-bag-shopping"></i>

                    <h3>Your bag is empty</h3>

                    <p>Add something delicious!</p>

                </div>

            `;

        }


        let total = 0;
        let quantity = 0;


        cart.forEach((item, index) => {

            total +=
                item.price * item.quantity;

            quantity += item.quantity;


            const div =
                document.createElement("div");

            div.className = "cart-item";

            div.innerHTML = `

                <img src="${item.image}"
                     alt="${item.name}">

                <div class="cart-item-info">

                    <h4>${item.name}</h4>

                    <span>
                        Rs. ${item.price.toLocaleString()}
                        × ${item.quantity}
                    </span>

                </div>

                <button
                    class="cart-remove"
                    data-index="${index}">

                    <i class="fa-solid fa-trash"></i>

                </button>

            `;

            cartItems.appendChild(div);

        });


        cartCount.textContent = quantity;

        cartTotal.textContent =
            `Rs. ${total.toLocaleString()}`;


        document
            .querySelectorAll(".cart-remove")
            .forEach(button => {

                button.addEventListener(
                    "click",
                    () => {

                        const index =
                            Number(
                                button.dataset.index
                            );

                        cart.splice(index, 1);

                        updateCart();

                    }
                );

            });

    }


    /* ================================================
       CHECKOUT
    ================================================ */

    const checkoutBtn =
        document.getElementById("checkoutBtn");

    const checkoutModal =
        document.getElementById("checkoutModal");

    const closeCheckout =
        document.getElementById("closeCheckout");

    checkoutBtn.addEventListener("click", () => {

        if (cart.length === 0) {

            showToast(
                "Please add a product first"
            );

            return;

        }

        checkoutModal.classList.add("show");

    });


    closeCheckout.addEventListener(
        "click",
        () => checkoutModal.classList.remove("show")
    );


    document
        .getElementById("checkoutForm")
        .addEventListener("submit", event => {

            event.preventDefault();

            checkoutModal.classList.remove("show");

            cart = [];

            updateCart();

            closeCartSidebar();

            showToast(
                "Order placed successfully! ❤️"
            );

            event.target.reset();

        });


    /* ================================================
       CUSTOM CAKE
    ================================================ */

    const customModal =
        document.getElementById("customModal");

    const customCakeBtn =
        document.getElementById("customCakeBtn");

    const closeCustom =
        document.getElementById("closeCustom");

    customCakeBtn.addEventListener(
        "click",
        () => customModal.classList.add("show")
    );

    closeCustom.addEventListener(
        "click",
        () => customModal.classList.remove("show")
    );


    document
        .getElementById("customForm")
        .addEventListener("submit", event => {

            event.preventDefault();

            customModal.classList.remove("show");

            showToast(
                "Custom cake request sent! 🎂"
            );

            event.target.reset();

        });


    /* ================================================
       CONTACT FORM
    ================================================ */

    document
        .getElementById("contactForm")
        .addEventListener("submit", event => {

            event.preventDefault();

            showToast(
                "Message sent successfully!"
            );

            event.target.reset();

        });


    /* ================================================
       NEWSLETTER
    ================================================ */

    document
        .getElementById("newsletterForm")
        .addEventListener("submit", event => {

            event.preventDefault();

            showToast(
                "You're subscribed! ❤️"
            );

            event.target.reset();

        });


    /* ================================================
       TOAST
    ================================================ */

    const toast =
        document.getElementById("toast");

    const toastMessage =
        document.getElementById("toastMessage");

    let toastTimer;


    function showToast(message) {

        toastMessage.textContent = message;

        toast.classList.add("show");

        clearTimeout(toastTimer);

        toastTimer =
            setTimeout(() => {

                toast.classList.remove("show");

            }, 3000);

    }


    /* ================================================
       CLOSE MODAL WHEN CLICKING OUTSIDE
    ================================================ */

    window.addEventListener("click", event => {

        if (event.target === checkoutModal) {
            checkoutModal.classList.remove("show");
        }

        if (event.target === customModal) {
            customModal.classList.remove("show");
        }

    });


    /* ================================================
       ESCAPE KEY
    ================================================ */

    document.addEventListener("keydown", event => {

        if (event.key === "Escape") {

            searchPanel.classList.remove("open");

            checkoutModal.classList.remove("show");

            customModal.classList.remove("show");

            closeCartSidebar();

        }

    });


    /* ================================================
       INITIAL CART
    ================================================ */

    updateCart();

});
