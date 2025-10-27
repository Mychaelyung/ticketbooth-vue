<template>
  <div id="app">
    <!-- Toast Notification -->
    <div v-if="toast" 
         :class="['fixed top-4 right-4 z-50 p-4 rounded-lg shadow-lg flex items-center gap-2',
                  toast.type === 'error' ? 'bg-red-500 text-white' : 'bg-green-500 text-white']">
      <component :is="toast.type === 'error' ? AlertCircleIcon : CheckCircleIcon" :size="20" />
      <span>{{ toast.message }}</span>
      <button @click="toast = null" class="ml-2">
        <XIcon :size="16" />
      </button>
    </div>

    <!-- Landing Page -->
    <div v-if="currentPage === 'landing'" class="min-h-screen bg-gradient-to-br from-blue-50 to-indigo-50">
      <!-- Navigation -->
      <nav class="bg-white shadow-sm">
        <div class="max-w-[1440px] mx-auto px-4 sm:px-6 lg:px-8">
          <div class="flex justify-between items-center h-16">
            <div class="flex items-center gap-2">
              <TicketIcon class="text-indigo-600" :size="28" />
              <span class="text-xl font-bold text-gray-900">TicketBooth</span>
            </div>
            <div class="hidden md:flex gap-4">
              <button @click="currentPage = 'login'" class="px-4 py-2 text-indigo-600 hover:text-indigo-800 font-medium">
                Login
              </button>
              <button @click="currentPage = 'signup'" class="px-6 py-2 bg-indigo-600 text-white rounded-lg hover:bg-indigo-700 font-medium">
                Get Started
              </button>
            </div>
            <button class="md:hidden" @click="mobileMenuOpen = !mobileMenuOpen">
              <MenuIcon :size="24" />
            </button>
          </div>
          <div v-if="mobileMenuOpen" class="md:hidden pb-4 flex flex-col gap-2">
            <button @click="currentPage = 'login'" class="px-4 py-2 text-indigo-600 hover:text-indigo-800 font-medium text-left">
              Login
            </button>
            <button @click="currentPage = 'signup'" class="px-4 py-2 bg-indigo-600 text-white rounded-lg hover:bg-indigo-700 font-medium">
              Get Started
            </button>
          </div>
        </div>
      </nav>

      <!-- Hero Section -->
      <div class="relative bg-gradient-to-r from-indigo-600 to-purple-600 text-white overflow-hidden">
        <div class="absolute top-10 right-10 w-64 h-64 bg-white opacity-10 rounded-full"></div>
        
        <div class="max-w-[1440px] mx-auto px-4 sm:px-6 lg:px-8 py-20 md:py-32 relative z-10">
          <div class="text-center max-w-3xl mx-auto">
            <h1 class="text-4xl md:text-6xl font-bold mb-6">
              Manage Your Tickets Effortlessly
            </h1>
            <p class="text-xl md:text-2xl mb-8 text-indigo-100">
              Streamline your workflow with our powerful ticket management system. Track, resolve, and organize tickets with ease.
            </p>
            <div class="flex flex-col sm:flex-row gap-4 justify-center">
              <button @click="currentPage = 'signup'" class="px-8 py-4 bg-white text-indigo-600 rounded-lg hover:bg-gray-100 font-bold text-lg shadow-lg">
                Get Started Free
              </button>
              <button @click="currentPage = 'login'" class="px-8 py-4 bg-transparent border-2 border-white text-white rounded-lg hover:bg-white hover:text-indigo-600 font-bold text-lg">
                Login
              </button>
            </div>
          </div>
        </div>

        <!-- Wave SVG -->
        <svg class="absolute bottom-0 left-0 w-full" viewBox="0 0 1440 120" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path d="M0,64 C240,96 480,96 720,64 C960,32 1200,32 1440,64 L1440,120 L0,120 Z" fill="#F9FAFB"/>
        </svg>
      </div>

      <!-- Features Section -->
      <div class="max-w-[1440px] mx-auto px-4 sm:px-6 lg:px-8 py-20">
        <h2 class="text-3xl md:text-4xl font-bold text-center mb-12 text-gray-900">
          Why Choose TicketBooth?
        </h2>
        <div class="grid md:grid-cols-3 gap-8">
          <div class="bg-white p-8 rounded-xl shadow-lg hover:shadow-xl transition-shadow relative">
            <div class="absolute -top-4 -right-4 w-24 h-24 bg-green-400 opacity-20 rounded-full"></div>
            <div class="w-12 h-12 bg-green-500 rounded-lg flex items-center justify-center mb-4">
              <TicketIcon class="text-white" :size="24" />
            </div>
            <h3 class="text-xl font-bold mb-3 text-gray-900">Easy Ticket Creation</h3>
            <p class="text-gray-600">
              Create and manage tickets in seconds with our intuitive interface. Track status and priority effortlessly.
            </p>
          </div>

          <div class="bg-white p-8 rounded-xl shadow-lg hover:shadow-xl transition-shadow relative">
            <div class="absolute -bottom-4 -left-4 w-32 h-32 bg-purple-400 opacity-20 rounded-full"></div>
            <div class="w-12 h-12 bg-purple-500 rounded-lg flex items-center justify-center mb-4">
              <ClockIcon class="text-white" :size="24" />
            </div>
            <h3 class="text-xl font-bold mb-3 text-gray-900">Real-time Updates</h3>
            <p class="text-gray-600">
              Stay informed with instant updates on ticket status changes and team activities.
            </p>
          </div>

          <div class="bg-white p-8 rounded-xl shadow-lg hover:shadow-xl transition-shadow">
            <div class="w-12 h-12 bg-indigo-500 rounded-lg flex items-center justify-center mb-4">
              <CheckSquareIcon class="text-white" :size="24" />
            </div>
            <h3 class="text-xl font-bold mb-3 text-gray-900">Complete Control</h3>
            <p class="text-gray-600">
              Full CRUD operations with validation, error handling, and a secure authentication system.
            </p>
          </div>
        </div>
      </div>

      <!-- Footer -->
      <footer class="bg-gray-900 text-white py-8">
        <div class="max-w-[1440px] mx-auto px-4 sm:px-6 lg:px-8 text-center">
          <p class="text-gray-400">© 2025 TicketBooth. All rights reserved.</p>
        </div>
      </footer>
    </div>

    <!-- Auth Pages -->
    <div v-else-if="currentPage === 'login' || currentPage === 'signup'" 
         class="min-h-screen bg-gradient-to-br from-blue-50 to-indigo-50 flex items-center justify-center px-4">
      <div class="max-w-md w-full bg-white rounded-xl shadow-xl p-8 relative">
        <div class="absolute -top-6 -right-6 w-32 h-32 bg-indigo-400 opacity-20 rounded-full"></div>
        
        <div class="text-center mb-8">
          <div class="flex justify-center mb-4">
            <TicketIcon class="text-indigo-600" :size="48" />
          </div>
          <h2 class="text-3xl font-bold text-gray-900">
            {{ currentPage === 'login' ? 'Welcome Back' : 'Create Account' }}
          </h2>
          <p class="text-gray-600 mt-2">
            {{ currentPage === 'login' ? 'Login to manage your tickets' : 'Sign up to get started' }}
          </p>
        </div>

        <form @submit.prevent="handleAuth" class="space-y-4">
          <div v-if="currentPage === 'signup'">
            <label class="block text-sm font-medium text-gray-700 mb-1">Name</label>
            <input v-model="authForm.name" type="text" 
                   class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-transparent" />
            <p v-if="authErrors.name" class="text-red-500 text-sm mt-1">{{ authErrors.name }}</p>
          </div>

          <div>
            <label class="block text-sm font-medium text-gray-700 mb-1">Email</label>
            <input v-model="authForm.email" type="email" 
                   class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-transparent" />
            <p v-if="authErrors.email" class="text-red-500 text-sm mt-1">{{ authErrors.email }}</p>
          </div>

          <div>
            <label class="block text-sm font-medium text-gray-700 mb-1">Password</label>
            <input v-model="authForm.password" type="password" 
                   class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-transparent" />
            <p v-if="authErrors.password" class="text-red-500 text-sm mt-1">{{ authErrors.password }}</p>
          </div>

          <button type="submit" class="w-full bg-indigo-600 text-white py-3 rounded-lg hover:bg-indigo-700 font-medium">
            {{ currentPage === 'login' ? 'Login' : 'Sign Up' }}
          </button>
        </form>

        <p class="text-center mt-6 text-gray-600">
          {{ currentPage === 'login' ? "Don't have an account? " : "Already have an account? " }}
          <button @click="currentPage = currentPage === 'login' ? 'signup' : 'login'" 
                  class="text-indigo-600 hover:text-indigo-800 font-medium">
            {{ currentPage === 'login' ? 'Sign Up' : 'Login' }}
          </button>
        </p>
      </div>
    </div>

    <!-- Dashboard -->
    <div v-else-if="currentPage === 'dashboard'" class="min-h-screen bg-gradient-to-br from-blue-50 to-indigo-50">
      <nav class="bg-white shadow-sm">
        <div class="max-w-[1440px] mx-auto px-4 sm:px-6 lg:px-8">
          <div class="flex justify-between items-center h-16">
            <div class="flex items-center gap-2">
              <TicketIcon class="text-indigo-600" :size="28" />
              <span class="text-xl font-bold text-gray-900">TicketBooth</span>
            </div>
            <button @click="handleLogout" class="flex items-center gap-2 px-4 py-2 text-red-600 hover:bg-red-50 rounded-lg">
              <LogOutIcon :size="20" />
              <span class="hidden sm:inline">Logout</span>
            </button>
          </div>
        </div>
      </nav>

      <div class="max-w-[1440px] mx-auto px-4 sm:px-6 lg:px-8 py-8">
        <div class="mb-8">
          <h1 class="text-3xl md:text-4xl font-bold text-gray-900 mb-2">Dashboard</h1>
          <p class="text-gray-600">Welcome back! Here's an overview of your tickets.</p>
        </div>

        <div class="grid sm:grid-cols-2 lg:grid-cols-4 gap-6 mb-8">
          <div class="bg-white p-6 rounded-xl shadow-md relative overflow-hidden">
            <div class="absolute top-0 right-0 w-20 h-20 bg-indigo-400 opacity-10 rounded-full -mr-10 -mt-10"></div>
            <div class="flex items-center justify-between">
              <div>
                <p class="text-gray-600 text-sm font-medium">Total Tickets</p>
                <p class="text-3xl font-bold text-gray-900 mt-1">{{ stats.total }}</p>
              </div>
              <div class="w-12 h-12 bg-indigo-100 rounded-lg flex items-center justify-center">
                <TicketIcon class="text-indigo-600" :size="24" />
              </div>
            </div>
          </div>

          <div class="bg-white p-6 rounded-xl shadow-md relative overflow-hidden">
            <div class="absolute bottom-0 left-0 w-24 h-24 bg-green-400 opacity-10 rounded-full -ml-12 -mb-12"></div>
            <div class="flex items-center justify-between">
              <div>
                <p class="text-gray-600 text-sm font-medium">Open</p>
                <p class="text-3xl font-bold text-green-600 mt-1">{{ stats.open }}</p>
              </div>
              <div class="w-12 h-12 bg-green-100 rounded-lg flex items-center justify-center">
                <AlertCircleIcon class="text-green-600" :size="24" />
              </div>
            </div>
          </div>

          <div class="bg-white p-6 rounded-xl shadow-md">
            <div class="flex items-center justify-between">
              <div>
                <p class="text-gray-600 text-sm font-medium">In Progress</p>
                <p class="text-3xl font-bold text-amber-600 mt-1">{{ stats.inProgress }}</p>
              </div>
              <div class="w-12 h-12 bg-amber-100 rounded-lg flex items-center justify-center">
                <ClockIcon class="text-amber-600" :size="24" />
              </div>
            </div>
          </div>

          <div class="bg-white p-6 rounded-xl shadow-md">
            <div class="flex items-center justify-between">
              <div>
                <p class="text-gray-600 text-sm font-medium">Closed</p>
                <p class="text-3xl font-bold text-gray-600 mt-1">{{ stats.closed }}</p>
              </div>
              <div class="w-12 h-12 bg-gray-100 rounded-lg flex items-center justify-center">
                <CheckCircleIcon class="text-gray-600" :size="24" />
              </div>
            </div>
          </div>
        </div>

        <div class="bg-gradient-to-r from-indigo-600 to-purple-600 p-8 rounded-xl shadow-lg text-white">
          <h2 class="text-2xl font-bold mb-2">Ready to manage tickets?</h2>
          <p class="mb-4 text-indigo-100">View, create, edit, and delete tickets with full control.</p>
          <button @click="currentPage = 'tickets'" 
                  class="px-6 py-3 bg-white text-indigo-600 rounded-lg hover:bg-gray-100 font-medium">
            Go to Ticket Management
          </button>
        </div>
      </div>

      <footer class="bg-gray-900 text-white py-8 mt-12">
        <div class="max-w-[1440px] mx-auto px-4 sm:px-6 lg:px-8 text-center">
          <p class="text-gray-400">© 2025 TicketBooth. All rights reserved.</p>
        </div>
      </footer>
    </div>

    <!-- Ticket Management -->
    <div v-else-if="currentPage === 'tickets'" class="min-h-screen bg-gradient-to-br from-blue-50 to-indigo-50">
      <nav class="bg-white shadow-sm">
        <div class="max-w-[1440px] mx-auto px-4 sm:px-6 lg:px-8">
          <div class="flex justify-between items-center h-16">
            <div class="flex items-center gap-4">
              <button @click="currentPage = 'dashboard'" class="flex items-center gap-2">
                <TicketIcon class="text-indigo-600" :size="28" />
                <span class="text-xl font-bold text-gray-900">TicketBooth</span>
              </button>
            </div>
            <button @click="handleLogout" class="flex items-center gap-2 px-4 py-2 text-red-600 hover:bg-red-50 rounded-lg">
              <LogOutIcon :size="20" />
              <span class="hidden sm:inline">Logout</span>
            </button>
          </div>
        </div>
      </nav>

      <div class="max-w-[1440px] mx-auto px-4 sm:px-6 lg:px-8 py-8">
        <div class="flex justify-between items-center mb-8">
          <div>
            <h1 class="text-3xl md:text-4xl font-bold text-gray-900 mb-2">Ticket Management</h1>
            <p class="text-gray-600">Create, view, edit, and delete your tickets.</p>
          </div>
          <button @click="showForm = !showForm" 
                  class="flex items-center gap-2 px-6 py-3 bg-indigo-600 text-white rounded-lg hover:bg-indigo-700 font-medium">
            <PlusIcon :size="20" />
            <span class="hidden sm:inline">New Ticket</span>
          </button>
        </div>

        <!-- Form -->
        <div v-if="showForm" class="bg-white p-6 rounded-xl shadow-lg mb-8">
          <h2 class="text-xl font-bold mb-4 text-gray-900">
            {{ editingTicket ? 'Edit Ticket' : 'Create New Ticket' }}
          </h2>
          <form @submit.prevent="handleSubmitTicket" class="space-y-4">
            <div>
              <label class="block text-sm font-medium text-gray-700 mb-1">
                Title <span class="text-red-500">*</span>
              </label>
              <input v-model="ticketForm.title" type="text" 
                     class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-transparent" />
              <p v-if="ticketErrors.title" class="text-red-500 text-sm mt-1">{{ ticketErrors.title }}</p>
            </div>

            <div>
              <label class="block text-sm font-medium text-gray-700 mb-1">Description</label>
              <textarea v-model="ticketForm.description" rows="3"
                        class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-transparent"></textarea>
              <p v-if="ticketErrors.description" class="text-red-500 text-sm mt-1">{{ ticketErrors.description }}</p>
            </div>

            <div class="grid sm:grid-cols-2 gap-4">
              <div>
                <label class="block text-sm font-medium text-gray-700 mb-1">
                  Status <span class="text-red-500">*</span>
                </label>
                <select v-model="ticketForm.status" 
                        class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-transparent">
                  <option value="open">Open</option>
                  <option value="in_progress">In Progress</option>
                  <option value="closed">Closed</option>
                </select>
                <p v-if="ticketErrors.status" class="text-red-500 text-sm mt-1">{{ ticketErrors.status }}</p>
              </div>

              <div>
                <label class="block text-sm font-medium text-gray-700 mb-1">Priority</label>
                <select v-model="ticketForm.priority" 
                        class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-indigo-500 focus:border-transparent">
                  <option value="low">Low</option>
                  <option value="medium">Medium</option>
                  <option value="high">High</option>
                </select>
              </div>
            </div>

            <div class="flex gap-4">
              <button type="submit" class="px-6 py-2 bg-indigo-600 text-white rounded-lg hover:bg-indigo-700 font-medium">
                {{ editingTicket ? 'Update' : 'Create' }}
              </button>
              <button type="button" @click="resetForm" 
                      class="px-6 py-2 bg-gray-200 text-gray-700 rounded-lg hover:bg-gray-300 font-medium">
                Cancel
              </button>
            </div>
          </form>
        </div>

        <!-- Tickets List -->
        <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
          <div v-if="tickets.length === 0" class="col-span-full bg-white p-12 rounded-xl shadow-md text-center">
            <TicketIcon class="mx-auto text-gray-400 mb-4" :size="48" />
            <p class="text-gray-600 text-lg">No tickets yet. Create your first ticket to get started!</p>
          </div>

          <div v-for="ticket in tickets" :key="ticket.id" 
               class="bg-white p-6 rounded-xl shadow-md hover:shadow-lg transition-shadow">
            <div class="flex justify-between items-start mb-3">
              <h3 class="text-lg font-bold text-gray-900 flex-1">{{ ticket.title }}</h3>
              <span :class="['px-3 py-1 rounded-full text-xs font-medium', getStatusColor(ticket.status)]">
                {{ getStatusLabel(ticket.status) }}
              </span>
            </div>
            
            <p v-if="ticket.description" class="text-gray-600 text-sm mb-4 line-clamp-3">{{ ticket.description }}</p>
            
            <div class="flex items-center justify-between pt-4 border-t border-gray-100">
              <span class="text-xs font-medium text-gray-500 uppercase">
                Priority: {{ ticket.priority }}
              </span>
              <div class="flex gap-2">
                <button @click="handleEdit(ticket)" class="p-2 text-indigo-600 hover:bg-indigo-50 rounded-lg" title="Edit">
                  <Edit2Icon :size="18" />
                </button>
                <button @click="handleDelete(ticket.id)" class="p-2 text-red-600 hover:bg-red-50 rounded-lg" title="Delete">
                  <Trash2Icon :size="18" />
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>

      <footer class="bg-gray-900 text-white py-8 mt-12">
        <div class="max-w-[1440px] mx-auto px-4 sm:px-6 lg:px-8 text-center">
          <p class="text-gray-400">© 2025 TicketBooth. All rights reserved.</p>
        </div>
      </footer>
    </div>
  </div>
</template>

<script>
import { 
  AlertCircle as AlertCircleIcon, 
  CheckCircle as CheckCircleIcon, 
  X as XIcon, 
  Plus as PlusIcon, 
  Edit2 as Edit2Icon, 
  Trash2 as Trash2Icon, 
  LogOut as LogOutIcon, 
  Ticket as TicketIcon, 
  Clock as ClockIcon, 
  CheckSquare as CheckSquareIcon, 
  Menu as MenuIcon 
} from 'lucide-vue-next';

export default {
  name: 'App',
  components: {
    AlertCircleIcon,
    CheckCircleIcon,
    XIcon,
    PlusIcon,
    Edit2Icon,
    Trash2Icon,
    LogOutIcon,
    TicketIcon,
    ClockIcon,
    CheckSquareIcon,
    MenuIcon
  },
  data() {
    return {
      currentPage: 'landing',
      mobileMenuOpen: false,
      toast: null,
      authForm: {
        name: '',
        email: '',
        password: ''
      },
      authErrors: {},
      tickets: [],
      showForm: false,
      editingTicket: null,
      ticketForm: {
        title: '',
        description: '',
        status: 'open',
        priority: 'medium'
      },
      ticketErrors: {}
    };
  },
  computed: {
    stats() {
      return {
        total: this.tickets.length,
        open: this.tickets.filter(t => t.status === 'open').length,
        inProgress: this.tickets.filter(t => t.status === 'in_progress').length,
        closed: this.tickets.filter(t => t.status === 'closed').length
      };
    }
  },
  mounted() {
    this.initializeRoute();
    this.loadTickets();
    
    // Handle browser back/forward buttons
    window.addEventListener('popstate', this.handlePopState);
  },
  beforeUnmount() {
    window.removeEventListener('popstate', this.handlePopState);
  },
  watch: {
    toast(newVal) {
      if (newVal) {
        setTimeout(() => {
          this.toast = null;
        }, 4000);
      }
    }
  },
  methods: {
    initializeRoute() {
      const path = window.location.pathname;
      const token = localStorage.getItem('ticketapp_session');
      
      // Route mapping with protection
      if (path === '/' || path === '/landing') {
        if (token) {
          this.navigate('/dashboard');
        } else {
          this.currentPage = 'landing';
        }
      } else if (path === '/auth/login') {
        this.currentPage = 'login';
      } else if (path === '/auth/signup') {
        this.currentPage = 'signup';
      } else if (path === '/dashboard') {
        if (!token) {
          this.navigate('/auth/login');
        } else {
          this.currentPage = 'dashboard';
        }
      } else if (path === '/tickets') {
        if (!token) {
          this.navigate('/auth/login');
        } else {
          this.currentPage = 'tickets';
        }
      } else {
        this.currentPage = 'landing';
      }
    },
    navigate(path) {
      const token = localStorage.getItem('ticketapp_session');
      
      // Protected route check
      if ((path === '/dashboard' || path === '/tickets') && !token) {
        window.history.pushState({}, '', '/auth/login');
        this.currentPage = 'login';
        return;
      }
      
      // Update URL and page
      window.history.pushState({}, '', path);
      
      if (path === '/' || path === '/landing') {
        this.currentPage = 'landing';
      } else if (path === '/auth/login') {
        this.currentPage = 'login';
      } else if (path === '/auth/signup') {
        this.currentPage = 'signup';
      } else if (path === '/dashboard') {
        this.currentPage = 'dashboard';
      } else if (path === '/tickets') {
        this.currentPage = 'tickets';
      }
    },
    handlePopState() {
      const path = window.location.pathname;
      const token = localStorage.getItem('ticketapp_session');
      
      if ((path === '/dashboard' || path === '/tickets') && !token) {
        this.navigate('/auth/login');
      } else {
        this.initializeRoute();
      }
    },
    handleNavigate(page) {
      const routes = {
        'landing': '/landing',
        'login': '/auth/login',
        'signup': '/auth/signup',
        'dashboard': '/dashboard',
        'tickets': '/tickets'
      };
      this.navigate(routes[page] || '/landing');
    },
    loadTickets() {
      const stored = localStorage.getItem('tickets');
      if (stored) {
        this.tickets = JSON.parse(stored);
      }
    },
    saveTickets(tickets) {
      localStorage.setItem('tickets', JSON.stringify(tickets));
      this.tickets = tickets;
    },
    validateAuth() {
      const errors = {};
      if (!this.authForm.email) {
        errors.email = 'Email is required';
      } else if (!/\S+@\S+\.\S+/.test(this.authForm.email)) {
        errors.email = 'Email is invalid';
      }
      if (!this.authForm.password) {
        errors.password = 'Password is required';
      } else if (this.authForm.password.length < 6) {
        errors.password = 'Password must be at least 6 characters';
      }
      if (this.currentPage === 'signup' && !this.authForm.name) {
        errors.name = 'Name is required';
      }
      this.authErrors = errors;
      return Object.keys(errors).length === 0;
    },
    handleAuth() {
      if (!this.validateAuth()) return;

      const token = 'mock-token-' + Date.now();
      localStorage.setItem('ticketapp_session', token);
      localStorage.setItem('user_email', this.authForm.email);
      this.toast = { 
        message: `${this.currentPage === 'login' ? 'Login' : 'Signup'} successful!`, 
        type: 'success' 
      };
      setTimeout(() => {
        this.currentPage = 'dashboard';
      }, 1000);
    },
    handleLogout() {
      localStorage.removeItem('ticketapp_session');
      localStorage.removeItem('user_email');
      this.currentPage = 'landing';
    },
    validateTicket() {
      const errors = {};
      if (!this.ticketForm.title.trim()) {
        errors.title = 'Title is required';
      }
      if (!['open', 'in_progress', 'closed'].includes(this.ticketForm.status)) {
        errors.status = 'Status must be open, in_progress, or closed';
      }
      if (this.ticketForm.description && this.ticketForm.description.length > 500) {
        errors.description = 'Description must be less than 500 characters';
      }
      this.ticketErrors = errors;
      return Object.keys(errors).length === 0;
    },
    handleSubmitTicket() {
      if (!this.validateTicket()) return;

      if (this.editingTicket) {
        const updated = this.tickets.map(t =>
          t.id === this.editingTicket.id ? { ...this.ticketForm, id: t.id } : t
        );
        this.saveTickets(updated);
        this.toast = { message: 'Ticket updated successfully!', type: 'success' };
      } else {
        const newTicket = { ...this.ticketForm, id: Date.now().toString() };
        this.saveTickets([...this.tickets, newTicket]);
        this.toast = { message: 'Ticket created successfully!', type: 'success' };
      }

      this.resetForm();
    },
    resetForm() {
      this.ticketForm = {
        title: '',
        description: '',
        status: 'open',
        priority: 'medium'
      };
      this.editingTicket = null;
      this.showForm = false;
      this.ticketErrors = {};
    },
    handleEdit(ticket) {
      this.ticketForm = { ...ticket };
      this.editingTicket = ticket;
      this.showForm = true;
    },
    handleDelete(id) {
      if (confirm('Are you sure you want to delete this ticket?')) {
        const filtered = this.tickets.filter(t => t.id !== id);
        this.saveTickets(filtered);
        this.toast = { message: 'Ticket deleted successfully!', type: 'success' };
      }
    },
    getStatusColor(status) {
      switch (status) {
        case 'open': return 'bg-green-100 text-green-800';
        case 'in_progress': return 'bg-amber-100 text-amber-800';
        case 'closed': return 'bg-gray-100 text-gray-800';
        default: return 'bg-gray-100 text-gray-800';
      }
    },
    getStatusLabel(status) {
      return status === 'in_progress' ? 'In Progress' : status.charAt(0).toUpperCase() + status.slice(1);
    }
  }
};
</script>

<style>
@import 'tailwindcss/base';
@import 'tailwindcss/components';
@import 'tailwindcss/utilities';

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', 'Roboto', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.line-clamp-3 {
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
</style>