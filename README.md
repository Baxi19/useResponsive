# useResponsive
React Custom Hook for handle Responsive Screens

### useResponsive.jsx
```javascript
import { useState, useEffect } from 'react';

const useResponsive = () => {
  const [windowSize, setWindowSize] = useState({
    width: undefined,
    height: undefined,
  });

  useEffect(() => {
    const handleResize = () => {
      setWindowSize({
        width: window.innerWidth,
        height: window.innerHeight,
      });
    }
    handleResize(); // initial check
    window.addEventListener('resize', handleResize);
    return () => window.removeEventListener('resize', handleResize);
  }, []);

  const isMobile = windowSize.width <= 480;
  const isBigMobile = windowSize.width > 480 && windowSize.width <= 768;
  const isTablet = windowSize.width > 768 && windowSize.width <= 1024;
  const isMiniDesktop = windowSize.width > 1024 && windowSize.width <= 1366;
  const isDesktop = windowSize.width > 1366 && windowSize.width <= 1920;
  const isTvOrBigScreen = windowSize.width > 1920;

  return {
    isMobile,
    isBigMobile,
    isTablet,
    isMiniDesktop,
    isDesktop,
    isTvOrBigScreen,
  };
}

export default useResponsive;

```

### How to use:
```javascript
import useResponsive from './useResponsive';

const MyComponent = () => {
  const { isMobile, isBigMobile, isTablet, isMiniDesktop, isDesktop, isTvOrBigScreen } = useResponsive();
  // use the boolean flags to conditionally render UI
  return (
    <div>
      {isMobile && 'Mobile UI'}
      {isBigMobile && 'Big Mobile UI'}
      {isTablet && 'Tablet UI'}
      {isMiniDesktop && 'Mini Desktop UI'}
      {isDesktop && 'Desktop UI'}
      {isTvOrBigScreen && 'TV or Big Screen UI'}
    </div>
  );
}

export default MyComponent;
```
