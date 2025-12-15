<template>
  <Toast />
</template>

<script>
import Toast from 'primevue/toast';
import { useToast } from 'primevue/usetoast';

export default {
  name: 'ToastService',
  components: {
    Toast
  },
  data() {
    return {
      toast: null
    };
  },
  created() {
    this.toast = useToast();
  },
  methods: {
    showSuccess(message) {
      this.toast.add({
        severity: 'success',
        summary: 'Success',
        detail: message,
        life: 3000
      });
    },
    
    showError(message) {
      this.toast.add({
        severity: 'error',
        summary: 'Error',
        detail: message,
        life: 4000
      });
    },
    
    showInfo(message) {
      this.toast.add({
        severity: 'info',
        summary: 'Info',
        detail: message,
        life: 3000
      });
    },
    
    showWarning(message) {
      this.toast.add({
        severity: 'warn',
        summary: 'Warning',
        detail: message,
        life: 4000
      });
    },
    
    showCustom(severity, summary, detail, life = 3000) {
      this.toast.add({
        severity: severity,
        summary: summary,
        detail: detail,
        life: life
      });
    }
  },
  expose: ['showSuccess', 'showError', 'showInfo', 'showWarning', 'showCustom']
};
</script>

<style>
/* Toast container */
.p-toast {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  max-width: 400px;
  width: 100%;
}

/* All toast messages have the same width */
.p-toast .p-toast-message {
  border-radius: 6px;
  margin: 10px;
  padding: 12px 16px;
  width: 350px;
  min-width: 350px;
  max-width: 350px;
  box-sizing: border-box;
  word-wrap: break-word;
  overflow-wrap: break-word;
}

/* Adjust icon spacing in toast content - FIXED VERTICAL ALIGNMENT */
.p-toast .p-toast-message .p-toast-message-content {
  display: flex;
  align-items: center !important;
  justify-content: space-between;
  width: 100%;
}

/* Fix the icon alignment */
.p-toast .p-toast-message .p-toast-message-icon {
  font-size: 1rem !important;
  width: 1.5rem !important;
  height: 1.5rem !important;
  margin-right: 12px !important;
  flex-shrink: 0;
  display: flex !important;
  align-items: center !important;
  justify-content: center !important;
}

/* Fix the close button alignment - REMOVED STROKE/BORDER */
.p-toast .p-toast-message .p-toast-icon-close {
  width: 1.5rem !important;
  height: 1.5rem !important;
  min-width: 1.5rem !important;
  min-height: 1.5rem !important;
  font-size: 0.875rem !important;
  margin-left: 12px !important;
  flex-shrink: 0;
  display: flex !important;
  align-items: center !important;
  justify-content: center !important;
  padding: 0 !important;
  line-height: 1 !important;
  border: none !important; /* Remove border */
  outline: none !important; /* Remove outline */
  box-shadow: none !important; /* Remove any shadow */
  background: transparent !important; /* Make background transparent */
}

/* Remove focus/hover states that might add borders */
.p-toast .p-toast-message .p-toast-icon-close:focus {
  outline: none !important;
  box-shadow: none !important;
  border: none !important;
}

.p-toast .p-toast-message .p-toast-icon-close:hover {
  background: rgba(0, 0, 0, 0.05) !important; /* Subtle hover effect */
  border: none !important;
  border-radius: 50% !important;
}

/* Make sure the X icon is centered inside the button */
.p-toast .p-toast-message .p-toast-icon-close .pi {
  margin: 0 !important;
  padding: 0 !important;
  line-height: 1 !important;
  display: flex !important;
  align-items: center !important;
  justify-content: center !important;
}

/* Toast message text container */
.p-toast .p-toast-message .p-toast-message-content .p-toast-message-text {
  margin-left: 0;
  flex: 1;
  min-width: 0;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

/* Ensure text wraps properly */
.p-toast .p-toast-message .p-toast-summary,
.p-toast .p-toast-message .p-toast-detail {
  display: block;
  width: 100%;
  word-wrap: break-word;
  overflow-wrap: break-word;
}

/* Success toast */
.p-toast .p-toast-message.p-toast-message-success {
  background: rgba(255, 255, 255, 0.95) !important;
  border: 1px solid #c49a6c !important;
  color: #000000 !important;
  backdrop-filter: blur(10px);
}

.p-toast .p-toast-message.p-toast-message-success .p-toast-message-icon,
.p-toast .p-toast-message.p-toast-message-success .p-toast-icon-close {
  color: #c49a6c !important;
}

/* Error toast */
.p-toast .p-toast-message.p-toast-message-error {
  background: rgba(255, 255, 255, 0.95) !important;
  border: 1px solid #f87171 !important;
  color: #000000 !important;
  backdrop-filter: blur(10px);
}

.p-toast .p-toast-message.p-toast-message-error .p-toast-message-icon,
.p-toast .p-toast-message.p-toast-message-error .p-toast-icon-close {
  color: #f87171 !important;
}

/* Info toast */
.p-toast .p-toast-message.p-toast-message-info {
  background: rgba(255, 255, 255, 0.95) !important;
  border: 1px solid #60a5fa !important;
  color: #000000 !important;
  backdrop-filter: blur(10px);
}

.p-toast .p-toast-message.p-toast-message-info .p-toast-message-icon,
.p-toast .p-toast-message.p-toast-message-info .p-toast-icon-close {
  color: #60a5fa !important;
}

/* Warning toast */
.p-toast .p-toast-message.p-toast-message-warn {
  background: rgba(255, 255, 255, 0.95) !important;
  border: 1px solid #fbbf24 !important;
  color: #000000 !important;
  backdrop-filter: blur(10px);
}

.p-toast .p-toast-message.p-toast-message-warn .p-toast-message-icon,
.p-toast .p-toast-message.p-toast-message-warn .p-toast-icon-close {
  color: #fbbf24 !important;
}

/* Make the toast summary text */
.p-toast .p-toast-message .p-toast-summary {
  font-weight: 600;
  font-size: 0.95rem;
  line-height: 1.3;
}

/* Make the toast detail text */
.p-toast .p-toast-message .p-toast-detail {
  font-size: 0.875rem;
  margin-top: 2px;
  line-height: 1.4;
}

/* Force vertical alignment for all content */
.p-toast .p-toast-message .p-toast-message-content > * {
  vertical-align: middle !important;
}

/* Ensure consistent height for all elements */
.p-toast .p-toast-message .p-toast-message-content {
  min-height: 24px;
}

/* Additional border removal for PrimeVue specific classes */
.p-toast .p-toast-message .p-toast-icon-close.p-button.p-button-text.p-button-rounded {
  border: none !important;
  outline: none !important;
}

/* Remove any border that might come from PrimeVue themes */
.p-toast .p-toast-message .p-toast-icon-close:not(:focus):not(:active) {
  border: none !important;
}

/* Responsive adjustments */
@media (max-width: 480px) {
  .p-toast {
    max-width: 90vw;
    left: 5vw;
    right: 5vw;
  }
  
  .p-toast .p-toast-message {
    width: 100% !important;
    min-width: 100% !important;
    max-width: 100% !important;
    margin: 10px 0;
  }
}
</style>