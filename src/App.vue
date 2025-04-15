<template>
  <div class="ab-testing-container">
    <h1>A/B Testing Implementation</h1>
    <div class="user-info">
      <p><strong>Your UUID:</strong> {{ userId }}</p>
      <p><strong>You are in:</strong> Group {{ userGroup }}</p>
    </div>
    <button class="group-button">{{ buttonText }}</button>
  </div>
</template>

<script>
import { v4 as uuidv4 } from 'uuid';

export default {
  name: 'AbTestingApp',
  data() {
    return {
      userId: '',
      userGroup: ''
    };
  },
  computed: {
    buttonText() {
      return `group ${this.userGroup}`;
    }
  },
  methods: {
    
    getUserId() {
      let id = localStorage.getItem('user_id');
      
      if (!id) {
        // Generate a new UUID for first-time users
        id = uuidv4();
        localStorage.setItem('user_id', id);
        console.log('Generated new UUID:', id);
      } else {
        console.log('Retrieved existing UUID:', id);
      }
      
      this.userId = id;
      return id;
    },
    
    determineUserGroup(id) {
      if (!id) {
        console.error('No UUID provided');
        return 'B'; // Default fallback
      }
      
      const lastChar = id.slice(-1).toUpperCase();
      
      if (lastChar >= 'A' && lastChar <= 'J') {
        this.userGroup = 'A';
      } else {
        this.userGroup = 'B';
      }
      
      console.log(`User assigned to Group ${this.userGroup} based on last character: ${lastChar}`);
      return this.userGroup;
    }
  },
  created() {
    // When component is created, get/generate UUID and determine group
    const id = this.getUserId();
    this.determineUserGroup(id);
  }
};
</script>

<style scoped>
.ab-testing-container {
  max-width: 600px;
  margin: 40px auto;
  padding: 20px;
  border: 1px solid #e2e2e2;
  border-radius: 8px;
  text-align: center;
}

.user-info {
  margin: 20px 0;
  padding: 15px;
  background-color: #f5f5f5;
  border-radius: 5px;
}

.group-button {
  padding: 10px 20px;
  font-size: 16px;
  background-color: #4caf50;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.group-button:hover {
  background-color: #45a049;
}
</style>