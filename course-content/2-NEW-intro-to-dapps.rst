=======================
Introduction to React
=======================

`View Completed PRODUCT REGISTRY Demo <TODO>`_


.. important::

  In this exercise, you’re going to get a crash course on the React library by building a simple product registry and voting application.
  
  You will become familiar with the fundamentals of React front-end development and be able to build an interactive React app from scratch!

----

1. Starting the Application
=======================================================

.. note::

  Begin instructions from within the VM(via VirtualBox) that was configured and run in `step 6 of the prerequisites <https://blg-dapp-fundamentals.readthedocs.io/en/blg-school-hack-4-change/course-content/prerequisites/general.html#start-the-vm>`_.

`Video Tutorial [1-2] <todo>`_

Open a new terminal window
-----------------------------

  - Click on the terminal icon in the left dock

Start the app
-----------------

  - Change directory into the ``blg/product-registry-01`` folder on the Desktop
    
    .. code-block:: bash

      cd Desktop/blg/product-registry-01

  - Start the server
    
    .. code-block:: bash

      npm start

  - *Example output:*

    .. code-block:: console

      ajl@x1c:~/Desktop/blg/product-registry-01$ npm start

      > product-registry-01@1.0.0 start /home/ajl/Desktop/blg/product-registry-01
      > live-server --host=localhost --port=3000 --middleware=./libraries/disable-browser-cache.js

      Serving "/home/ajl/Desktop/blg/product-registry-01" at http://localhost:3000 (http://127.0.0.1:3000)
      Ready for changes

  - Chrome should automatically be opened and the application rendered!  Otherwise navigate to http://localhost:3000 in your browser.  
    You should see some basic text and your first task!

  .. image:: https://raw.githubusercontent.com/Blockchain-Learning-Group/course-resources/master/product-registry-01/images/01-completed-app.png

  .. note::

    The ``npm start`` command that you executed ran the ``start`` script in the included ``package.json`` file:
    
    .. code-block:: json

      {
        [...],
        "scripts": {
          "start": "live-server --host=localhost --port=3000 --middleware=./libraries/disable-browser-cache.js"
        },
        "devDependencies": {
          "live-server": "https://github.com/acco/live-server/tarball/master"
        }
      }
    
    This ran a very light-weight server that will host the code for your browser to access.
    The server will also detect changes in the code base and automatically re-render the browser.  
    Therefore you will not need to restart the server at all during development and every time that 
    you change and save a file the browser will render the updated page for you.

----

2. Understanding and Updating the Application
=======================================================

Open the application's code in the Sublime text editor
---------------------------------------------------------
- Open the Sublime text editor by clicking on the Sublime icon in the left dock.

- From within Sublime open the `product-registry-01` folder. 
- Click on ``File`` in the top left corner and select ``Open Folder...`` in the menu.  
- Select ``Desktop/blg/product-registry-01`` to open, and we can get to coding!

Open up the ``index.html`` file within the ``product-registry-01`` folder
------------------------------------------------------

  - View the contents of the file. 
  - Don't worry too much about what is being *linked* within the ``<head>`` of the file, the core to focus on is between the ``<body></body>`` tags beneath
  - The core of the application may be simplified to the following:

    .. code-block:: html

      <div>
        <h1>Welcome! Your first task, CHANGE ME :)</h1>
        <div id="content"></div>
      </div>
    
    - Simply a title ``<h1>`` and one ``<div>`` that contains the *content* of the application.  Remember this *content* ``<div>`` as we will see it again soon!

  - Update the title ``<h1></h1>`` where your first task is noted
  - Update the title to be **your** Product registry, for example ``Adam's Product Registry``

  - Example Code:

    .. code-block:: html

      <h1 class="ui dividing centered header">Adam's Product Registry</h1>

  - Save the file!  This may be done by selecting the File menu in the top left corner and selecting save, or with the keyboard shortcut ``ctrl + s```
  - View the updated title in the browser!  

  .. image:: https://raw.githubusercontent.com/Blockchain-Learning-Group/course-resources/master/product-registry-01/images/02-renamed-header.png

  - |index02|

    .. |index02| raw:: html

      <a href="https://github.com/Blockchain-Learning-Group/course-resources/blob/master/product-registry-01/dev-stages/index-02.html" target="_blank">Complete solution may be found here</a>


Reverting to a Blank ``app.js`` file to get started!
----------------------------------------------------
  
  - Note within the open ``index.html`` file that ``app-complete.js`` is linked in a ``<script>`` tag within the ``<body>``
  - Update this to link ``app.js`` instead of ``app-complete.js``, which is the blank template you will begin with.
  - Don't forget to save!

  - Example Code:

    .. code-block:: html

      <script
        type="text/babel"
        data-plugins="transform-class-properties"
        src="app.js"
      ></script>

  - |index03|

  .. |index03| raw:: html

    <a href="https://github.com/Blockchain-Learning-Group/course-resources/blob/master/product-registry-01/dev-stages/index-03.html" target="_blank">Complete solution may be found here</a>

3. Your First Component!
=========================================

.. note::

  **Components**

  - React components are entirely comprised of components. A component can be thought of as a UI element within an application, generally within your browser.
  - Components may be thought of as small self contained building blocks that may effectively be reused and combined within other to build up complete applications.
  - The layout, logic, and specific styles are all housed within the given self-contanied component.

Taking a look into ``app.js`` and a first component
----------------------------

  - The remainder of coding for this exercise will occur in the ``app.js`` file.  Go ahead and open that one up in the Sublime text editor.
  - It should contain the following *component*:

    .. code-block:: html

      class ProductRegistry extends React.Component {
        render() {
          return (
            <div className='ui unstackable items'>
              Hello, I am your first React component!
            </div>
          );
        }
      }

  - A React component is simply a JavaScript class, one which extends, or inherits from, the base React Component class
  - The ``React`` object is availble globally as the ``React`` library was in fact linked in the ``<head>`` of the ``index.html`` file: 

    .. code-block:: html

      <script src="libraries/react.js"></script>

  - The class, which we will refer to as a component moving forward, ``ProductRegistry`` has only a single function, ``render()``.  This is a required function and is
    used to determine what the component will render within the browser.
  - However, the return value doesn’t look like traditional JavaScript, and you are right as we are actually using ``JSX (JavaScript eXtension syntax)``, an extension for JavaScript. 
    JSX allows us to write the markup for our component views in a familiar, HTML-esq syntax.
  - Note the familiar looking ``<div>`` section within the return statement.  These are the elements that will be rendered in the browser.
  - Also note that although this file is now linked in your ``index.html`` it is not currently displayed in the browser. The text *"Hello, ..."* is not present
  
Rendering your component
--------------------------

  - You now have your first component defined and it is even linked in your ``index.html`` file... but it is not being rendered on the page... let's fix that.

    .. code-block:: html

      <script src="app.js"></script>

  - Remember that *content* ``<div>``?  Yes, we want to render our JSX component within that ``<div>`` on our page.  
  - Add the following lines at the bottom of your ``app.js`` file:

    .. code-block:: html

      ReactDOM.render(
        <ProductRegistry />,
        document.getElementById('content')
      );

  - Save the file and have a look at your browser. Is a warm hello from your component present?
  - Great, you have rendered your first React component!
  
  - *ReactDOM* is a package that the React library provides to essentially allow direct interaction with the elements defined in your ``index.html``.
  - Above you told React to locate the element on the current page(document) with the id *content* and to render the ``<ProductRegistry />`` component within it.
    Telling React *what* you want to render and *where* you want to render it, and voila it appeared beneath your title as is defined in your ``index.html``.
    
    Effectively resulting in the following:

    .. code-block:: html

      <div>
        <h1>Product Registry</h1>
        <div id="content">
          <ProductRegistry />
        </div>
      </div>

  .. image:: https://raw.githubusercontent.com/Blockchain-Learning-Group/course-resources/master/product-registry-01/images/03-hello.png

  - |app02|

  .. |app02| raw:: html

    <a href="https://github.com/Blockchain-Learning-Group/course-resources/blob/master/product-registry-01/dev-stages/app-02.js" target="_blank">Complete solution may be found here</a>

  .. important::

    Understanding |babel_link| and how our browser is able to understand your new JSX component.

    .. |babel_link| raw:: html

      <a href="https://babeljs.io/" target="_blank">Babel</a>

    Modern browsers' execution engines do not natively understand the JSX language.  JSX is an extension to standard JavaScript, which browsers do understand. 
    We therefore need to *translate* this JSX code to standard JavaScript so our browser can understand it.  
    Essentially your component is speaking Espanol while our browser only understands English.

    Babel is here to solve this problem for us!

    Babel is a JavaScript *transpiler*, or in more familiar English language a translator. Babel understands JSX and is capable of translating 
    your JSX into standard JavaScript.  You simply need to instruct the browser to use Babel prior to attemtping to execute the JSX code.

    The Babel library has been included in your ``index.html``:

    .. code-block:: html

      <script src="libraries/babel-standalone.js"></script>

    Finally the browser may be instructed to use Babel directly where the ``app.js`` file is linked in your ``index.html``:

      .. code-block:: html

        <script
          type="text/babel"
          data-plugins="transform-class-properties"
          src="app.js"
        ></script>
    
4. Creating the ``<Product>`` Component
=================================
.. note::

  A best practise in designing web application front ends, and especially when utilizing the ReactJS library, is to breakdown the final design into 
  modular, portable and reusable components.
  
  - |final_image|

    .. |final_image| raw:: html

      <a href="https://raw.githubusercontent.com/Blockchain-Learning-Group/course-resources/master/product-registry-01/images/01-completed-app.png" target="_blank">Have a look back at the final interface.</a> 

  Take a second and think about the components that you could break this up into.  Remembering that thus far we have defined the ``<ProductRegistry>``.

- Can the interface be simplified to a ``<ProductRegistry>`` of ``<Products>``?  We think so!
.. image:: https://raw.githubusercontent.com/Blockchain-Learning-Group/course-resources/master/product-registry-01/images/04-Product-Registry-UI-Component-Breakdown.png

- Navigate back to your open ``app.js`` file in your text editor.  It should currently look like this:

  .. code-block:: html

    class ProductRegistry extends React.Component {
      render() {
        return (
          <div className='ui unstackable items'>
            Hello, I am your first React component!
          </div>
        );
      }
    }

    ReactDOM.render(
      <ProductRegistry />,
      document.getElementById('content')
    );

- Begin by defining a brand new component, JavaScript class, beneath the existing ``<ProductRegistry>`` component

  .. code-block:: html

    class Product extends React.Component {}

- This is a completely empty component that will not render anything and in fact will throw an error as a ``render()`` function is required for each component.
  This is the function that defines what is to be rendered by the browser and by default empty components are not allowed.

- Add a ``render()`` function to the ``<Product>`` component to return a simple ``<div>`` saying "hello"

  .. code-block:: html

    class Product extends React.Component {
      render() {
        return (
          <div>Hello I am a product.</div>
        );
      }
    }

- Now remember what is currently being rendered to the page: 

  .. code-block:: html

    ReactDOM.render(
      <ProductRegistry />,
      document.getElementById('content')
    );

- Therefore the ``<Product>`` component is not being rendered yet and will not be present in the browser

- Add the ``<Product>`` component to the components that are returned by your ``<ProductRegistry>`` within the ``app.js`` file

  .. code-block:: html

    class ProductRegistry extends React.Component {
      render() {
        return (
          <div className='ui unstackable items'>
            Hello, I am your first React component!
            <Product />
          </div>
        );
      }
    }

.. image:: https://raw.githubusercontent.com/Blockchain-Learning-Group/course-resources/master/product-registry-01/images/05-product-added.png

- |app03|

  .. |app03| raw:: html

    <a href="https://github.com/Blockchain-Learning-Group/course-resources/blob/master/product-registry-01/dev-stages/app-03.js" target="_blank">Complete solution may be found here</a>

5. Building out Your Products
=================================

- Great work so far!  However, the application is not looking overly interesting just yet.  In this section you will build out the ``<Product>`` component.

.. note::

  |semantec_url|

    .. |semantec_url| raw:: html
    
    <a href="https://react.semantic-ui.com/" target="_blank">Semantic UI</a> 
  
  is being used as a styling library which has been linked in your ``index.html`` file for you. Therefore, the ``className`` reference in several of the
  elements below are in fact utilizing classes and styling that is provided by Semantic.

- Begin by extending the content that is returned by the component in it's ``render()`` function. 
  You will add an image, a title, a description, and an image of who submitted the product.

  .. code-block:: html

    class Product extends React.Component {
      render() {
        return (
          <div className='item'>
            <div className='image'>
              <img src='images/products/image-aqua.png' />
            </div>
            <div className='middle aligned content'>
              <div className='description'>
                <a>YOUR PRODUCT NAME</a>
                <p>NEW FANCY PRODUCT OF YOUR OWN</p>
              </div>
              <div className='extra'>
                <span>Submitted by:</span>
                <img className='ui avatar image' src='images/avatars/liz.png' />
              </div>
            </div>
          </div>
        );
      }
    }

- The image links in the component above map to the images that have been provided for you within the ``/images`` folder.
- The product image: ``<img src='images/products/image-aqua.png' />`` and the submitted image: ``<img className='ui avatar image' src='images/avatars/liz.png' />``
  both exist within their respective folders ``images/products/`` and ``images/avatars/``, feel free to add new images of your own and update these paths accordingly!

.. image:: https://raw.githubusercontent.com/Blockchain-Learning-Group/course-resources/master/product-registry-01/images/06-product-updated-images.png

- |app04|

  .. |app04| raw:: html

    <a href="https://github.com/Blockchain-Learning-Group/course-resources/blob/master/product-registry-01/dev-stages/app-04.js" target="_blank">Complete solution may be found here</a>

6. Loading Your Product List
=================================

- Currently your ``<Product>`` is completely hardcoded and although it may seem quite portable where you can place it just about anywhere, and may create 
  many instances of it, that is where the functionality ends.  That ``<Product>`` will currently always have the exact same images and text.
  This section will take you through the process of making the content of your components dynamic and allow them to be passed in as variables!

- Review your existing ``<Product>`` and have a look at the data fields that are present:

  1. Product Image URL:

    .. code-block:: html
    
        <div className='image'>
          <img src='images/products/image-aqua.png' />
        </div>

  2. Product Title:

    .. code-block:: html

      <div className='description'>
        <a>YOUR PRODUCT NAME</a>
        ...
      </div>

  3. Product Description:

    .. code-block:: html

      <div className='description'>
        ...
        <p>NEW FANCY PRODUCT OF YOUR OWN</p>
      </div>

  4. Submitted Image URL:

    .. code-block:: html

      <div className='extra'>
        <span>Submitted by:</span>
        <img className='ui avatar image' src='images/avatars/liz.png' />
      </div>

- Therefore a minimal representation of the data fields that are required for a ``<Product>`` at this time are:

  .. code-block:: JavaScript

    product = {
      title:              'YOUR PRODUCT NAME',
      description:        'YOUR PRODUCT DESCRIPTINON.',
      submitterAvatarUrl: 'images/avatars/adam.jpg',
      productImageUrl:    'images/products/image-aqua.png',
    }

- Open up the file ``seed.js`` and have a look around. Observe the definition of the array, or list, of products.
- Note there are 2 additional fields we did not previously define, ``id`` and ``votes``, which we will see in action shortly.

  .. code-block:: JavaScript

    const products = [
      {
        id: 1,
        title: 'Digi-Collectibles',
        description: 'The rarest digital collectibles.',
        votes: generateVoteCount(),
        submitterAvatarUrl: 'images/avatars/adam.jpg',
        productImageUrl: 'images/products/image-aqua.png',
      },
      ...
    ]

- This file defines a list of components that are to populate, or seed, the application when it initially renders.  This will take a few steps, 
  first you will need to update your ``<Product>`` component to allow data for it's fields to be passed in.

Making your ``<Product>`` dynamic
----------------------------

.. note::

  In order to do this we must introduce another ReactJS concept, that is **Props**.

  Components are allowed to accpet data passed to them from their *parents* meaning the components that contain them.  In your case the parent
  is the ``<ProductRegistry>`` and it may have many child ``<Product>`` s.  Therefore the ``<Product>`` components may accept data passed to them
  by the ``<ProductRegistry>``, and it is this data, passed from parent to child, that is referred to as *props*.  Essentially the input parameters 
  that a component may accept are referred to as *props*.

- Time to update your ``<Product>`` component to accept some props!

  1. Update Product Image URL:

    .. code-block:: html
    
        <div className='image'>
          <img src='images/products/image-aqua.png' />
        </div>

    to >>

    .. code-block:: html

        <div className='image'>
          <img src={this.props.productImageUrl} />
        </div>

  2. Product Title:

    .. code-block:: html

      <div className='description'>
        <a>YOUR PRODUCT NAME</a>
        ...
      </div>

    to >>

    .. code-block:: html

      <div className='description'>
        <a>{this.props.title}</a>
        ...
      </div>

  3. Product Description:

    .. code-block:: html

      <div className='description'>
        ...
        <p>NEW FANCY PRODUCT OF YOUR OWN</p>
      </div>

    to >>

    .. code-block:: html

      <div className='description'>
        ...
        <p>{this.props.description}</p>
      </div>

  4. Submitted Image URL:

    .. code-block:: html

      <div className='extra'>
        <span>Submitted by:</span>
        <img className='ui avatar image' src='images/avatars/liz.png' />
      </div>

    to >>

    .. code-block:: html

      <div className='extra'>
        <span>Submitted by:</span>
        <img className='ui avatar image' src={this.props.submitterAvatarUrl} />
      </div>

- The resulting component should look like the following:

  .. code-block:: html

    class Product extends React.Component {
      render() {
        return (
          <div className='item'>
            <div className='image'>
              <img src={this.props.productImageUrl} />
            </div>
            <div className='middle aligned content'>
              <div className='description'>
                <a>{this.props.title}</a>
                <p>{this.props.description}</p>
              </div>
              <div className='extra'>
                <span>Submitted by:</span>
                <img className='ui avatar image' src={this.props.submitterAvatarUrl} />
              </div>
            </div>
          </div>
        );
      }
    }

- This may look odd at first, seeing JavaScript directly inline with html, and that is in fact the beauty of JSX! The ``{}`` braces identify
  that what is within them is a JavaScript expression.  Therefore the props object of the ``<Product>`` component(remember just a JavaScript class).
- You will notice immediately that the rendered ``<Product>`` is currently empty as there are no props being passed in to the component now to every
  data field is in fact empty.  Let's fix that and get your hands on some data.

- |app05|

  .. |app05| raw:: html

    <a href="https://github.com/Blockchain-Learning-Group/course-resources/blob/master/product-registry-01/dev-stages/app-05.js" target="_blank">Complete solution may be found here</a>

Understanding ``seed.js`` and the ``window``
--------------------------------------

- Take a look back at the ``seed.js`` file that should be open at this time, if it is not do open it now.  This is where our data is going to come from!
- Let's walk through this file one step at a time ...

  .. note::

    JavaScript exposes a top level object accessible with the ``window`` keyword which represents the browser window.  This object contains many functions
    and properties about the given browser session and also allows you as a developer to bind data to the window that may be globally accessible.

    Let's have a look at this ``window`` object directly in the browser to see what it is all about.

    - Right-click in your browser and in the dropdown menu select *inspect*.
    - Within the console type ``window`` and hit enter.
    - You will see a reference to the global ``window`` object, expand this and have a look around.  This is the top level object that JavaScript natively 
      exposes.

    .. image:: https://raw.githubusercontent.com/Blockchain-Learning-Group/course-resources/master/product-registry-01/images/07-dev-console-window.png

- The first line of ``seed.js`` is in fact accessing this ``window`` object and adding an attribute to it: ``Seed``.

  .. code-block:: JavaScript
    
    window.Seed = (function () {...});

- This attribute is set to a ``function()`` and this function returns an object: ``{ products: products }``.  
  Resulting in: ``window.Seed = { products: products }``
- Where ``products`` is your array of product data fields:

  .. code-block:: JavaScript

    const products = [
      {
        id: 1,
        title: 'Digi-Collectibles',
        description: 'The rarest digital collectibles.',
        votes: generateVoteCount(),
        submitterAvatarUrl: 'images/avatars/adam.jpg',
        productImageUrl: 'images/products/image-aqua.png',
      },
      ...
    ]

- Have a look at this attribute back in the browser.  
- In the browser console type ``window.Seed`` and you will see the result!  
- Yes, all of your data has been loaded and is availble globally attached to the ``window`` object.  
- In fact every ``window`` attribute is accessible without the ``window`` keyword as they are added
  to the global scope of the application.  Therefore this object may simply be accessed globally via just ``Seed``.

  .. code-block:: JavaScript

    > window.Seed
      > {products: Array(4)}

    > Seed
      > {products: Array(4)}

Loading a product from the Seed
--------------------------------

- Now it is time to utilize this seed data to populate your ``<Product>``
- Within the ``<ProductRegistry>`` component load the first product of the Seed data into a local variable. Remember it is the parent that must pass
  the data to the child, ``<Product>``, as props.

  .. code-block:: html

    class ProductRegistry extends React.Component {
      render() {
        const product = Seed.products[0];

        return (
          <div className='ui unstackable items'>
            Hello, I am your first React component!
            <Product />
          </div>
        );
      }
    }

- Pass the seed data to the ``<Product>`` component as props:

  .. code-block:: html

    <Product
      title={product.title}
      description={product.description}
      submitterAvatarUrl={product.submitterAvatarUrl}
      productImageUrl={product.productImageUrl}
    />

- You can also get rid of the "Hello..." line that is currently in the ``<ProductRegistry>`` resulting with the following component:

  .. code-block:: html

    class ProductRegistry extends React.Component {
      render() {
        const product = Seed.products[0];

        return (
          <div className='ui unstackable items'>
            <Product
              title={product.title}
              description={product.description}
              submitterAvatarUrl={product.submitterAvatarUrl}
              productImageUrl={product.productImageUrl}
            />
          </div>
        );
      }
    }

.. image:: https://raw.githubusercontent.com/Blockchain-Learning-Group/course-resources/master/product-registry-01/images/08-seed-product-data.png

- |app06|

  .. |app06| raw:: html

    <a href="https://github.com/Blockchain-Learning-Group/course-resources/blob/master/product-registry-01/dev-stages/app-06.js" target="_blank">Complete solution may be found here</a>



TITLE
=================================


.. image:: https://raw.githubusercontent.com/Blockchain-Learning-Group/course-resources/master/product-registry-01/images/

- |solution_link|

  .. |solution_link| raw:: html

    <a href="https://github.com/Blockchain-Learning-Group/course-resources/blob/master/product-registry-01/dev-stages/app-.js" target="_blank">Complete solution may be found here</a>
