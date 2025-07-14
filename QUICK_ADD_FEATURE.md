# Quick Add Feature for Product Recommendations

## Overview
This feature adds a "Quick Add" button to product recommendations that allows customers to quickly add products to their cart or open a product popup for variant selection.

## Features

### 1. Quick Add Button
- **Location**: Appears on product recommendation cards
- **Behavior**: 
  - For single-variant products: Directly adds to cart
  - For multi-variant products: Opens a popup for variant selection
- **Visibility**: 
  - Desktop: Appears on hover
  - Mobile: Always visible
- **Styling**: Semi-transparent overlay with backdrop blur effect

### 2. Implementation Details

#### Files Modified:
- `snippets/product-item-recommendation.liquid` - New product item snippet with quick add functionality
- `sections/product-recommendations.liquid` - Updated to use new snippet
- `sections/cart-recommendations.liquid` - Updated to use new snippet
- `sections/mini-cart.liquid` - Updated to use new snippet
- `sections/recently-viewed-products.liquid` - Updated to use new snippet

#### Key Features:
- **Responsive Design**: Adapts to different screen sizes
- **Accessibility**: Proper focus states and ARIA labels
- **Performance**: Uses existing Shopify quick buy components
- **SEO Friendly**: Maintains existing product structure

### 3. Button Behavior

#### Single Variant Products:
```liquid
{%- form 'product', product, is: 'product-form' -%}
  <input type="hidden" name="quantity" value="1">
  <input type="hidden" name="id" value="{{ product.first_available_variant.id }}">
  <button type="submit">{{ 'collection.product.add_to_cart_short' | t }}</button>
{%- endform -%}
```

#### Multi-Variant Products:
```liquid
<button is="toggle-button" aria-controls="product-recommendation-{{ section.id }}-{{ product.id }}-popover">
  {{ 'collection.product.quick_view' | t }}
</button>
<quick-buy-popover href="{{ product.url }}?view=quick-buy-popover"></quick-buy-popover>
```

### 4. Styling

#### CSS Features:
- **Hover Effects**: Smooth transitions and elevation
- **Backdrop Blur**: Modern glass-morphism effect
- **Responsive**: Different sizes for mobile/desktop
- **Accessibility**: Focus states and proper contrast

#### Key CSS Classes:
- `.product-item__quick-add-wrapper` - Container for the button
- `.product-item__quick-add-button` - The actual button
- `.product-item__image-wrapper` - Parent container for positioning

### 5. Usage

The feature is automatically applied to:
- Product page recommendations
- Cart page recommendations  
- Mini-cart recommendations
- Recently viewed products

### 6. Customization

#### To modify button text:
Edit the translation keys in `locales/` files:
- `collection.product.add_to_cart_short`
- `collection.product.quick_view`

#### To change styling:
Modify the CSS in `snippets/product-item-recommendation.liquid`

#### To disable for specific products:
Add the condition `hide_secondary_image != true` to the quick add wrapper

### 7. Browser Support
- Modern browsers with backdrop-filter support
- Graceful fallback for older browsers
- Mobile-optimized touch interactions

### 8. Performance Considerations
- Uses existing Shopify quick buy components
- No additional JavaScript required
- Minimal CSS overhead
- Lazy loading compatible

## Technical Notes

### Dependencies:
- Shopify's built-in quick buy functionality
- Existing theme CSS variables
- Product form components

### SEO Impact:
- Maintains existing product structure
- No impact on search engine crawling
- Preserves product links and metadata

### Accessibility:
- Proper ARIA labels
- Keyboard navigation support
- Focus management
- Screen reader compatible 